Character
- Soul 
	- inputs
		- kb
		- mouse
		- controller
	- AI
		- pathfinding
		- following
		- intelligence/strategy (npc)
- Brain (Action State Machine)
	- walk
	- run
	- jump
	- sit
	- crouch
	- slide
	- wallrun
- Body (visuals and physics)
	- model
		- mesh
		- skeleton
		- texture
		- collision
	- animationplayer
	- Health
- Senses
	- Eyes (Camera)
		- 1st Person
		- 2nd Person
		- 3rd Person
		- GUI
	- Tongue (Dialogue System)
	- Ears (Audio System client)
	- Nose (detection system)
		- area detection
		- staircase raycasts
	- Touch (Interaction system)
	- 6th Sense (External Signals Client)
	- Sense Extention
		- weapons
		- guns
		- items
		- tools


**Soul** tells the **Brain** what to do, whether it be inputs from the player or some form of artificial intelligence system. 
**Brain** tells the **Body** what action to perform. maybe a combination of actions or a series of actions. 
**Body** holds the physical body of the character and will manipulate it to perform the different actions.
**Senses** is a way for the character to interact with the world or for the world to interact with the player. 


Example. 
**Soul** says move from a to b quickly
**Brain** converts it to run with speed=5 from position a to position b
**Body** triggers the run animation and move_and_slide() from (x1, y1, z1) to (x2, y2, z2) at speed=5

