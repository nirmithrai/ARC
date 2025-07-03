```dataviewjs
// === CONFIG ===
const ROOT_NOTE = "INTERESTS.md";  
const PRESENT_RX = /^#+\s+Present$/i; // any depth "# Present"
const DBG = [];

async function crawl(filePath, seen = new Set()) {
  if (seen.has(filePath)) return { links: new Set(), tasks: [] };
  seen.add(filePath);

  // ---- read raw lines ----
  const fileObj = app.vault.getAbstractFileByPath(filePath);
  if (!fileObj) return { links: new Set(), tasks: [] };
  const lines = (await app.vault.cachedRead(fileObj)).split("\n");

  let inPresent = false;
  const links = new Set();

  for (const line of lines) {
    if (/^\s*#+\s/.test(line)) {
      inPresent = PRESENT_RX.test(line);  
      continue;
    }
    if (!inPresent) continue;

    for (const [, target] of line.matchAll(/\[([^|]+?)(?:\|[^\]]+)?\]\]/g))
      links.add(target);
  }

  const tasks = [];
  const page = dv.page(filePath);
  page?.file?.tasks?.forEach(t => {
    if (t.section?.subpath?.match(/Present$/i)) tasks.push(t);
  });
	DBG.push({ file: filePath, tasksFound: tasks.length }); 

  for (const l of [...links]) {
    const dest = app.metadataCache.getFirstLinkpathDest(l, filePath);
    if (dest) {
      const { links: moreLinks, tasks: moreTasks } =
        await crawl(dest.path, seen);
      moreLinks.forEach(x => links.add(x));
      tasks.push(...moreTasks);
    }
  }
  return { links, tasks };
}

// === run ===
const root = app.metadataCache.getFirstLinkpathDest(
  ROOT_NOTE,
  dv.current().file.path
);
if (!root) {
  dv.paragraph(`⚠️ Could not find ${ROOT_NOTE}.md`);
  return;
}

const interest_links = dv.page(ROOT_NOTE).file.outlinks[0]


const { links, tasks } = await crawl(root.path);
dv.table(["File","Tasks"], DBG.map(r => [r.file, r.tasksFound]));
// === output ===
dv.header(3, "⏳ Current Focus");
dv.list([...links].map(p => dv.fileLink(p)));

dv.header(3, "📝 Open Tasks");
dv.taskList(tasks, false);
```

---

```dataviewjs
const ROOT_NOTE = "Notes/INTERESTS.md";  
let log = []

async function crawl(filePath, seen = new Set()) {
	const links = new Set()
	const tasks = []
	
	return {links, tasks}
}

const interests = dv.page(ROOT_NOTE).file.outlinks

interests.forEach(interest => {
	//log.push(interest)
	const pg = dv.page(interest)
	const lists = pg?.file?.lists
	if (!pg) return [];
	log.push(lists.text)
	
})

const { links, tasks } = await crawl(ROOT_NOTE)

// dv.el('b',interests)
dv.paragraph(log)

```

---

```dataviewjs
/*****************************************************************
 * DASHBOARD : recursively collect every link that sits inside a
 *             “# Present” section, starting from INTERESTS.md
 *****************************************************************/
const ROOT_NOTE  = "INTERESTS";    // full path if it lives in a folder
const TARGET_HDR = "present";      // lowercase for comparison
const DBG = [];
/* ---------- load the root note ---------- */
const root = dv.page(ROOT_NOTE);
if (!root) {
  dv.paragraph(`⚠️ Missing root page: "${ROOT_NOTE}.md". Check the path.`);
} else {

  /* ---------- helpers ---------- */
  // For one page, return array of wikilink paths that are physically
  // located inside any # Present section.
  function linksUnderPresent(pagePath) {
    const pg = dv.page(pagePath);
    if (!pg) return [];

    // Find every Present-section range [startLine, endLine)
    const ranges = [];
    const secs   = pg.file.lists.section;
	DBG.push(pagePath)
	DBG.push(pg.file)
    secs && secs.forEach((s, i) => {
    //DBG.push(s)
      if (s.heading && s.heading.toLowerCase() === TARGET_HDR) {
        const start = s.position.start.line;
        const end   = (i + 1 < secs.length)
                    ? secs[i + 1].position.start.line
                    : Infinity;
        ranges.push([start, end]);
      }
    });

    // Keep only out-links that fall inside one of those ranges
    return pg.file.outlinks.filter(l => ranges.some(([a,b]) => l.position.start.line >= a && l.position.start.line < b)).map(l => l.path);
  }

  /* ---------- BFS crawl ---------- */
  const queue   = root.file.outlinks.array().map(l => l.path);  // first-level interests
  const visited = new Set(queue);
  const edges   = [];                                    // { parent, child }

  while (queue.length) {
    const current = queue.pop();
    for (const child of linksUnderPresent(current)) {
    DBG.push(child)
      edges.push({ parent: current, child });
      if (!visited.has(child)) {
        visited.add(child);
        queue.push(child);
      }
    }
  }

  /* ---------- render ---------- */
  dv.list(
    edges
      .sort((a, b) => a.child.localeCompare(b.child))
      .map(e => `[[${e.child}]] (from [[${e.parent}]])`)
  );
}
//dv.list(DBG)

```
