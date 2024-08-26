---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 12
---

> [!info]- What is Raycasting?
> Raycasting is an alternative to firing projectiles in your game. Projectiles (bullets, lasers etc) that have a ‘physical’ object being fired in the game take up processing power, memory etc. Raycasting is a more efficient method of determining if shots hit, or if an object can see another etc.

> [!info] You can implement raycasting into your game without impacting existing functionality for shooting or another purpose,

# Input Map

First, you can choose to create a new input trigger for raycasting. Go to Project → Project Settings → Input Map and create a new input map called `raycast` and assign a key to it.

> [!info] In this example the key `r` has been assigned. You can choose another key or mouse button as required.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastAddInput.png]]

# Player Object

Open the Player object (`Player.tscn`) and create a **RayCast3D** child object of the Camera node.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastAddChild.png]]

With RayCast3D selected, set the Enabled option to be true in the Inspector. Additionally, get the **Target Position** settings to  `0, 0, -10`. This will set the ray cast to be set to be in the direction of the camera.

> [!tip] You should see the raycast line aiming in the same direction of the camera. If not you may need to change these settings. 

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastSetDirection.png]]



Create a `MeshInstance3D` as a child of the Player root node, calling it **HitPoint**.

![raycastHitPoint](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/raycastHitPoint.png)

In the inspector, Create a new SphereMesh, and change the radius and height to 0.1 and 0.2 respectively. 

Set the colour of the mesh to red (or any other colour) to make it stand out in the game.

![raycastHitPointColour](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/raycastHitPointColour.png)


Move the sphere along the Z axis to represent where the raycast is aiming towards. Notice the blue line to represent the raycast.

![raycastHitPointPosition](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/raycastHitPointPosition.png)

Save the `Player.tscn` file.

# `Player.gd` script

Open `Player.gd` and add two new variables at the top of the script to store connection to the raycast nodes.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastVariableDeclaration.png]]

```gdscript
@onready var ray = $Camera3D/RayCast3D
```

Update `_physics_process()` to include a check to see if the user has pressed the `raycast` input.

If they have, then the code will check to see if the raycast is actually colliding with a collider.

If it does collide with a collider, then it will check if that object has a function called `raycast_collision()` in it’s script (to be written later). If it does, run that function.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastPlayerScriptDetect.png]]

```gdscript
if Input.is_action_pressed("raycast"):
	if ray.is_colliding():
		var collider = ray.get_collider()
		
		if collider:
			#print("Collided with " + collider.name + " at %s " % ray.get_collision_point())
			if collider.has_method("raycast_collision"):
				collider.raycast_collision()
```


# Modifying objects

For objects to be detected by raycasts in this implementation there **must** be two things:

- a collider on the object.
- the parent object **must** have a script with a `raycast_collision()` function included.

## Enemy Example

In order to detect the Enemy object with raycasts, you will need to add a RigidBody3D and another CollisionShape3D to the object.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastEnemyChildNodes.png]]

Add a CapsuleShape3D to the newCollisionShape3D

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastEnemyAddShape.png]]

Edit `enemy.gd` to add the new function which will run with a raycast detection.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastEnemyCollision.png]]

```gdscript
func raycast_collision():
	print("ray hit")
	
```



## Wall Example

Objects can be quickly edited to add a CSG shape, such as `CSGBox3D` enabled for collisions. For example, the wall objects can be modified to include this.

![[ISD/2 - Digital Applications/_topics/tutorials/images/rayCastWallUseCollision.png]]

Attach a script to the Wall root node. Include the function and at this stage simply output that the raycast has been detected.

```gdscript
func raycast_collision():
	print("ray hit")
```

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastWallScript.png]]

Save the Wall scene and script.

When the game is now run, aim at a wall and press the `ray` input. The “ray hit” output should be visible in the Output.

![[ISD/2 - Digital Applications/_topics/tutorials/images/raycastOutput.png]]

Any other objects in the game can react to raycasts but following the same process of adding a collider as a child, such as a `CSGBox3D`, and including a script with a `raycast_collision()` function included.

The `raycast_collision()` can delete the object, add points etc - whatever you need the object to do when it is “shot”.

![[commonBlocks#Commit & Push]]