
https://github.com/TinyTakinTeller/TakinGodotTemplate


# to switch the game
the main is the res://root/scene/game_scene/game_content folder
that's where my main game scene will live. its called game_content.tscn in the template. 

in the game_scene.tscn you can add the main game scene as a node. call it GameContent or change the path in game_scene.gd.
make sure that
- project.godot, .godot, .git files are deleted. else godot will consider it a different project and so not show it in this one. 
- addons are move and activated
- autoloads are added