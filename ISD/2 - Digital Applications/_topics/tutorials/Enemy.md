---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 6
---

Every FPS needs an enemy!

# Create a Scene

Create a new scene (`File`→ `New Scene`) and create the root node as a `RigidBody3D`. This will be the root node of the enemy object.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyNewRoot.png]]
![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyCharacterBody3d.png]]

Rename the node as `Enemy`.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyRename.png]]

Add a `MeshInstance3D` as a child of `Enemy`.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyAddMeshInstance3D.png]]

Click on the down arrow next to Mesh and choose New CapsuleMesh.

> [!note] This can be created as whatever type of object you wish, or a custom Mesh.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyNewCapsule.png]]

Ensure that the capsule is *vertical*. This simulates the character's body, so needs to stand upright. If the capsule is not vertical, change the rotate values to make it look like this.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyVerticalCapsule.png]]

# Timer

Add a Timer node as a child of enemy.
![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyNewTimer.png]]

With the Timer selected, set the wait time to something appropriate and set it to Autostart.

In this case, the enemy will wait 2 seconds before starting to move towards the player.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyTimerSettings.png]]


# Collision Shape

The last step is to create a Collision Shape (hitbox) for it to interact with other objects in the game.

Create a `CollisionShape3D` child node of Enemy.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyCollisionShape3D.png]]

With the CollisionShape3D selected, set the Shape attribute to a Capsule.

> [!note] If you set the MeshInstance3D to be any other shape than a capsule, you may need to modify this step to match.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyCollsionShape.png]]

# Navigation Agent
The next node to add is `NavigationAgent3D`. This is the node that will interact with the NavigationMesh created in another stage.

![enemyNavAgent](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/enemyNavAgent.png)

# Script

Attach a new Script to the enemy node.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyAttachScript.png]]

Replace the script with the following code.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyScript.png]]

```gdscript
extends CharacterBody3D

@onready var nav_agent = $NavigationAgent3D
var SPEED = 3.0

func update_target_location (target_location):
	nav_agent.set_target_position(target_location)

func _physics_process(delta):
	var current_location = global_transform.origin
	var next_location = nav_agent.get_next_path_position()
	look_at(next_location) # Enemy will turn to face player
	
	# Vector Maths
	var new_veloicty = (next_location-current_location).normalized() * SPEED

	velocity = new_veloicty
	
	move_and_slide()
	
```

# Add Enemy Group

With the main enemy node selected, set the group to `enemy`.

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemyGroup.png]]


# Save The Scene

Save the scene as `enemy.tscn`. 

![[ISD/2 - Digital Applications/_topics/tutorials/images/enemySaveScene.png]]


![[commonBlocks#Commit & Push]]