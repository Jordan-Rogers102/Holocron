
## Game Play

  
![[https://www.youtube.com/watch?v=nQfOhc6jumE](https://www.youtube.com/watch?v=nQfOhc6jumE)


This video shows the process of designing and coding the fundamental gameplay of space invaders.  

## Border Containment

  

![https://youtu.be/ef0R6-4viOA](https://youtu.be/ef0R6-4viOA)

  

In this video, you're shown how to create (invisible) borders on the left and right of the screen using Area2D nodes, and assigning them groups.

  

Then, the player object is modified to add it's own Area2D so that you can detect collisions between the object and the newly created borders.

  

Finally, you're shown the code to restrict the player to the playing area between the two borders.

  

## Global Variables & Bullets

  

![https://youtu.be/cYXn_vcRRTk](https://youtu.be/cYXn_vcRRTk)

  

In this video you're shown how to create global variables. Global Variables can be accessed (used) by any script throughout the entire project, from any script. This can be used to keep track of many variables needed throughout the project, such as the high score, or in the case of this video - the limiting the number of bullets on screen at once.

  
## bullet.gd

```GDScript

extends KinematicBody2D

var speed = 500

# Called when the node enters the scene tree for the first time.

func _ready():
	GlobalVariables.bulletInstanceCount += 1
	set_physics_process(true)

func _physics_process(delta):
	var collidedObject = move_and_collide(Vector2(0, -speed*delta))
	if (collidedObject):
		#print(collidedObject.collider.name)
		if "Enemy" in collidedObject.collider.name:
			collidedObject.get_collider().queue_free()
			queue_free()
		GlobalVariables.bulletInstanceCount -= 1

```
![[commonBlocks#Commit & Push]]