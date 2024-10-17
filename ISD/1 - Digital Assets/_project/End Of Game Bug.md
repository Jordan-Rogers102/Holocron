
If your game is experiencing a bug where objects from the Main Game are appearing after a scene changes, such as when the player dies or countdown finishes, this is one method of fixing the bug.

In `Global.gd` add a new variable called `Player`. This variable will be used as a ‘pointer’ to the player object. When the player object gets created, the `Player` variable will set to point to the player object. When the scene ends (win or lose) the `Player` variable will be set back to null.

Save the Script.

  ![[newVariablePlayer.png]]

  

In `[Player.gd](http://Player.gd)` update `_ready()` set the `GlobalVariables.Player` to be the Player object. This uses the `self` keyword.

  ![[setPlayerToSelf.png]]


```gdscript
GlobalVariables.Player = self
```

  

For ******all****** objects that need to be deleted from the game when the player dies or the player wins (i.e. the scene needs to change), add the following code to the **********start********** of the `_process()` or `_physics_process(delta)` functions

  

Repeat this for all objects. You may need to add this code to `enemy.gd` , `Bullet.gd`, and `Bullet-Enemy.gd` scripts.

![[checkPlayerNull.png]]  
  

```gdscript
if GlobalVariables.Player == null:
	queue_free()
```

  

Finally, Whenever the player object or game finished, set the `GlobalVariables.Player` variable back to `null`.
  

This will need to be added to any point where the scene changes in the main game. For instance, when the countdown finishes.

  ![[setPlayerNull.png]]


  

```gdscript
GlobalVariables.Player = null
```

![[commonBlocks#Commit & Push]]