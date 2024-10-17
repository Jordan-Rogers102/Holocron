

```
Raycasts are an invisible line between two points in game. Using Raycasts you can detect collisions (or potential collisions). They have a number of uses such as calculating the destination of a bullet, without creating (instantiating) a bullet in game, or if an object can ‘see’ another object (if there’s a wall in the way).
```
  

In the project, open the `enemy.tscn` file to edit the enemy object. This will update **all** enemy instances in the game.


Add a child node to the Enemy. Search for RayCast2D in the list and choose Create.

  ![[newNodeRayCast2D.png]]


  

With the new RayCast2D node selected, change the Inspector values `Enabled` and `Cast To:.`

  
![[raycastEnable.png]]
  

Attach a script to the RayCast2D node.

  
![[raycastAttachScript.png]]


  
![[raycastSetRaycastName.png]]


  

Replace the contents with the following code.

  

Save the script.

  

```gdscript

extends RayCast2D

# Called when the node enters the scene tree for the first time.

func _ready():
	set_process(true)

  

func _process(delta):
	if self.is_colliding():
		get_parent().canShoot = false
	else:
		get_parent().canShoot = true

```

  

Open Enemy.gd and create a new variable, declaring it at the top of the script.

  

```gdscript
var canShoot = false
```

  
![[raycastCanShoot.png]]


  

**Update** the _process() function to first check if canShoot is true. If it is true, then the normal ‘shooting’ code will execute.

  
> You only need to add the following line to the function - `if canShoot:`.

  
![[raycastIfCanShoot.png]]

![[commonBlocks#Commit & Push]]