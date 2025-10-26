Character
- Soul 
	- kbController
	- mouseController
	- gamepadController
	- AIController
		- pathfinding
		- following
		- intelligence/strategy (npc)
	- ReplayController
	- NetworkController
- Brain
	- LocomotionAbilities
		- walk (locomotion layer)
		- run (locomotion layer)
		- jump (locomotion layer)
		- wallrun (locomotion layer)
	- UpperBodyAbilities
		- punch
	- ModesSystem
		- sit (mode layer)
		- crouch (mode layer)
		- prone (mode layer)
		- clamber
- Body (physics driven)
	- CharacterBody3D
	- Skeleton3D
	- AnimationTree
	- VFX emitter
	- SFX emitter
	- Hitboxes
	- Hurtboxes
	- Collisions
- Senses
	- Eyes (Camera)
		- 1st Person
		- 2nd Person (dialogue)
		- 3rd Person
		- 4th Person (cutscenes)?
		- GUI
	- Tongue (Dialogue System)
	- Ears (Audio System client)
	- Nose (detection system)
		- area detection
	- Feet (raycasts for stairs, terrain detection)
	- Touch (Interaction system)
	- 6th Sense (External Signals Client)
		- wall surfaces broadcasting “runnable”
		- 
- Extensions
	- swords
		- UpperBodyAbilities
			- light attack (upperbody layer)
			- heavy attack (upperbody layer)
			- stab (upperbody layer)
	- guns
		- LocomotionAbilities
			- slide
		- UpperBodyAbilities
			- aim
			- reload
			- shoot
			- melee
		- ModesSystem
			- lean
			- peek
	- items (potion, scroll)
	- rope (item example)
		- ModesSystem
			- climb
		- StaminaSystem (running out of stamina)
	- tools (pickaxe, torch)
- Knowledge
	- DefaultStats
	- CurrentStats 
	- LevelingSystem
	- HealthSystem
	- StaminaSystem
	- StatusEffects
		- burn
		- wet
		- cold
		- exhaustion
- Memory
	- sense observations
	- npc/enemy tracking
	- env context
		- footing
		- ledges
		- next corner
	- history
		- damage history
		- npc interacted
	- tag handler
- DebugHUD
	- stats
	- soul info
	- brain info
	- body info
	- senses info
	- tag inspector



**Soul** tells the **Brain** what to do, whether it be inputs from the player or some form of artificial intelligence system. 
**Brain** tells the **Body** what action to perform. maybe a combination of actions or a series of actions. 
**Body** holds the physical body of the character and will manipulate it to perform the different actions.
**Senses** is a way for the character to interact with the world or for the world to interact with the player. 


Example. 
**Soul** says move from a to b quickly
**Brain** converts it to run with speed=5 from position a to position b
**Body** triggers the run animation and move_and_slide() from (x1, y1, z1) to (x2, y2, z2) at speed=5

Soul to Brain - Command
Sense to Knowledge - Observation

## One-page rubric for “where does this live?”

- Does it decide _whether_ an action can happen? **Brain**.
- Does it change numbers or add/remove tags? **Knowledge systems** (Health/Stamina/StatusEffects).
- Does it sense the world? **Senses**.
- Does it move meshes/colliders, play anim/VFX/SFX? **Body**.
- Is it player/AI/network input? **Soul**.
- Is it only available because of gear? **Extensions** (which register abilities/modifiers).