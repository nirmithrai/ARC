```dataviewjs
// === CONFIG ===
const ROOT_NOTE = "INTERESTS.md";  
const PRESENT_RX = /^#+\s+Present$/i; // any depth "# Present"

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

const { links, tasks } = await crawl(root.path);

// === output ===
dv.header(3, "⏳ Current Focus");
dv.list([...links].map(p => dv.fileLink(p)));

dv.header(3, "📝 Open Tasks");
dv.taskList(tasks, false);
```


