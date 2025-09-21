https://github.com/Phazorknight/Cogito

data-driven inventory, menus, interactables, quests; very clean scene/service split and mostly GDScript. Great for seeing many systems talk cleanly

# Notes 1
Reading the description, seems like a fully fledged game framework. its got a bit of everything. If i wanted to quickly make a game, this would be a really good option to start with. I may still do that, but i want to study how they handle all these different systems. 
- What kind of patterns do they use?
- how do they handle composition/inheritance?
- signals?
- how do they handle the controls and rebinding them
- how does inventory based resources work?
- what about the UI layer?
- they support dialogic and dialogue manager, what kind of support is it? is it just a matter of not getting in its way or is there special provisions for these plugins? what is the difference between the two plugin?

## Video tutorials on how the project works
https://cogito.readthedocs.io/en/latest/tutorials.html

1. feature reel
object interactions seem cool. exactly what i had in mind for mine
crafting system is there too. 
RE style inventory management
physics based puzzle like portal
this is a very good project. makes me wonder why i'm bothering with mine. i should just use this project to make whatever game comes to mind. 
but the problem comes during debugging. if you dont know how it works, its hard to fix it. 
my goal is to learn game development right now, not making games. if i just wanted to make games, this would be an excellent template to start from. i might still just steal from this project. its a very good base to start from. 

2. pickups vs items vs wieldable
Pickup is the 3D representation of the Inventory Item resource. + Actions makes them wieldable, ie gun, sword.

3. Localization
**POT file**. and POT generation. apparently a standard way of handling localization. Need to research more on this. 
There are other ways to handle translations as well

Next is a whole tutorial series, i wont watch them all, but seems like its just tutorials on how each aspect of the framework works. 

## Reading the Docs
look like there is a plugin dependency on **Quick Audio** and **Input Helper**. good to know

> The root node of your level scene needs to have `cogito_scene.gd` attached

i should check what that script holds. seems super useful.

component design pattern. 
>most functions are organized in a way where you will have a root node of an object, and can add or remove several child nodes as _Components_ to change the object’s behavior. For example:
>- Player scene has Attributes as child nodes.
>- Cogito Objects have InteractionComponents as child nodes.

Composition over inheritance then. 

its a "bring your own assets" kinda deal. they have scripts for common stuff 
`cogito_door.gd` -> scene root
BasicInteration - additional nodes/components -> child nodes


*FAQ section*
https://cogito.readthedocs.io/en/latest/faq.html#how-do-i-get-a-reference-to-the-player
good thing to know. referencing the player is always a pain in the ass. they offer 3 solutions
1. send the player body in the method/signal params. (double check with player group)
2. player group
3. their scene manager autoload
one thing i hadn't considered was having all 3 and using whatever is most convenient at that time 


Next actually looking at the code
# Notes 2
before i get to cogito, i'm looking at **quick_audio** plugin that the was a prerequisite. i noticed a cool pattern. 

```gdscript
if not (audio_stream_player_out is AudioStreamPlayer or audio_stream_player_out is AudioStreamPlayer2D or audio_stream_player_out is AudioStreamPlayer3D):
	push_error("Non-AudioStreamPlayer[XD] provided to Audio.sequential_fade(...) as audio_stream_player_out")
	return

```

an "if not" pattern for validation. 
```psuedo
if not (things i want to be true):
	error(msg)
	return
```

this is such a simple thing that i never considered. i do a lot of 
!loading?Component:Loading  
and this is very similar, but it is something i just didn't consider. 

**input_helper**
it is interesting to see how plugins are made. seems like essentially just \_enter_tree() and \_exit_tree() functions adding and removing an autoload. 

input_helper.gd is a huge file. not going to look at the whole thing. 

skimmed through it, only thing i got from this was that i should NOT be trying to write everything myself. there are a lot of exceptions and corner cases and modes and conditions that will take me months if not years to sort out. i really should be using existing projects to make my life easier. 

does this mean that i should use cogito itself? idk. i think if i were to make a game, i really should use it. but im not trying to make a game, i'm trying to learn game development. so i should look at different aspects and decided whether it's worth writing all this code myself. 

[[STEAL]]. 

im going to steal to accelerate my progress. im going to find the best [[basic 3d movement]] system and steal it, im going to find the best [[basic camera system]] and steal it. im going to find the best [[inventory system]] and steal it. i dont want to write everything myself. but i do want everything to be mine. i'll relentlessly steal code from all the sources i can find and then make them my own. 


Next time. Actually looking at Cogito's code. fr fr

# Notes 3
