
To enable health in the player, a few scripts need to be updated. Open `Player.gd` and add a new function at the bottom of the script to reduce the health of the player.

  

> Depending on your requirements, you can change the value that health is reduced by.

  
![[reduceHealth.png]]


```gdscript

func reduceHealth():
	health -= 1
	if health == 0:
		get_tree().change_scene("res://Menu/Menu.tscn")

```

  

At the top of the script, add a new variable called `health` which can also be configured in the Godot IDE by including the `export` keyword.

  ![[newVariableHealth.png]]


  

```gdscript

export (int) var health = 1

```

  

Save the script.

  

Open `Bullet-Enemy.gd` and update the code which runs when the bullet collides with an option. This code will check if the collidedObject contains the word “Player”, and if so, run the `reduceHealth()` function on that object.

  

Save the script.

  ![[detectPlayerCollision.png]]

  

```gdscript

if "Player" in collidedObject.collider.name:
	collidedObject.collider.reduceHealth()
```

  

Test the functionality.

  
![[commonBlocks#Commit & Push]]

  