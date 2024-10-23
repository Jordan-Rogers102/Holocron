---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 10
---

This stage of the tutorial will demonstrate how to implement a simple health system, where there is a player health and when the enemy collides with the player, the health reduces. As with many other aspects of game development, the exact implementation will depend on the requirements for the project, so apply as necessary.

> [!note] This process can be applied to ANY object that you wish to reduce the players health when a collision occurs.

# Player Script

## Create Health Variable

Open `Player.gd` and add a new variable named `player_health`. Set the initial value to be 100.

Save the file.

![[playerHealthVariable.png]]

# Detect Collision

> [!info]- Detect the collision from the enemy.
> The reason that the collision is detected from the enemy's perspective rather than the Player object is that the collision is only detected when the object is moving. 
> So, for instance, if the player is standing still, and the enemy collides with it, if the player is checking for a collision it won't be triggered as the player wasn't the one moving.

Open the `enemy.gd` script and update the `_physics_process` function to detect collisions with other objects in the game. This is done **after** the `move_and_slide` function call. 

This code checks to see what objects the enemy is colliding with, and if one of those is named "Player", then call the `reduce_health` function on that player (defined below).
 
![[playerHealthEnemyDetectCollision.png]]
 
```gdscript
for i in get_slide_collision_count():
	var collision = get_slide_collision(i)
	#print("I collided with ", collision.get_collider().name)
	if "Player" in collision.get_collider().name:
		collision.get_collider().reduce_health(10)
```

Finally, once the Enemy collides with the player and reduces health, you would most likely want the enemy to die so it doesn't continue to reduce health. Add a `queue_free()` to the code.

![[playerHealthQueueFree.png]]

Save the script.

# Lose Scene

If not already done, create a new scene and save it as `Lose.tscn`. This scene will be loaded if the player has lost, or in this example, run out of health.

![[playerHealthLoseScene.png]]

Design the scene in whichever way you wish, just ensure there is a way for the user to return to the main menu.

# Reduce Health function

Open `Player.gd`.
To standardise the process for removing health from the player, create a new function to handle the steps. Call the function similar to this: `reduce_health(10)`

![[playerHealthReduceHealthFunction.png]]

```gdscript
func reduce_health(amount):
	player_health -= amount
```

## Players death

In the new function, add a check to see if the players health reaches 0, and if so, end the game.

![[playerHealthDeath.png]]

```gdscript
if player_health < 0:
	# The player dies. 
	# Go back to the main menu. This can be changed to any scene in the future.
	get_tree().change_scene_to_file("res://Menus/main_menu.tscn")
```

Save the script.

![[commonBlocks#Commit & Push]]