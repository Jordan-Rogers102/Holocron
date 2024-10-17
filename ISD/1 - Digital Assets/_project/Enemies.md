
Enemy Group Movement

  

![https://youtu.be/Hav91wHl3JA](https://youtu.be/Hav91wHl3JA)

  

In this video, you're shown how to group the enemy instances together and script them to "bounce" off the sides of the game window when the first collision occurs.

  
## Enemies.gd

```GDScript

extends Node2D

var speed = -200

func _ready():
	set_physics_process(true)
	func _physics_process(delta):
	global_position.x += speed * delta

```

  

## Enemies Firing

  

![https://youtu.be/9XiSX3SM428](https://youtu.be/9XiSX3SM428)

  

In this first video, you're shown the configuration of the enemy bullets, and walked through the changes that need to be made to the `global.gd`, `enemy.gd` scripts and the creation of the `enemy-bullets.gd` script.

  

## Bullet-enemy.gd

```GDScript

extends KinematicBody2D

var speed = 500

# Called when the node enters the scene tree for the first time.
func _ready():
	GlobalVariables.enemyBulletInstanceCount += 1
	set_physics_process(true)

func _physics_process(delta):
	var collidedObject = move_and_collide(Vector2(0, +speed*delta*0.4))
	if (collidedObject):
		#print("Enemy collide: ",collidedObject.collider.name)
		if "Enemy" in collidedObject.collider.name:
		pass
		#collidedObject.get_collider().queue_free() #Don't kill the enemies.
	
	else:
		queue_free()
		GlobalVariables.enemyBulletInstanceCount -= 1
		print("Enemy Bullets: ", GlobalVariables.enemyBulletInstanceCount)
```

## Enemy.gd

```GDScript

extends KinematicBody2D

var bullet = preload("res://Bullet-Enemy/Bullet-Enemy.tscn")

func _ready():
	$Area2D.connect("area_entered", self, "_colliding")

func _colliding(area):

	if area.is_in_group("right"):
		#print("emenies collide right")
		get_parent().global_position.y += 10
		get_parent().speed = -200
	
	if area.is_in_group("left"):
		#print("emenies collide left")
		get_parent().global_position.y += 10
		get_parent().speed = 200

func _process(delta):
	var rng = RandomNumberGenerator.new()
	rng.randomize()
	var my_random_number = rng.randf_range(2.0, 30.0)
	#print("time: ",my_random_number)
	yield(get_tree().create_timer(my_random_number), "timeout")
	if GlobalVariables.enemyBulletInstanceCount < 5:
		var bulletInstance = bullet.instance()
		bulletInstance.position = Vector2(global_position.x, global_position.y+20)
		get_tree().get_root().add_child(bulletInstance)

```
## Global.gd

``` GDScript

extends Node

var bulletInstanceCount = 0 # Keeps track of how many bullet instances are current

var enemyBulletInstanceCount = 0

```

  ![[commonBlocks#Commit & Push]]