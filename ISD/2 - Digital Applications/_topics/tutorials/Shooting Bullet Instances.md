---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 5
---


> [!note]- **Prerequisites** 
> A bullet (or any projectile) scene needs to have been created and saved according to the instructions given on this site. If you have created your own method, you will have to adapt this as necessary.

With the bullet created, the game now needs to be configured to *shoot* the bullet. Initially, this will be done in the player script.

First, the code will need to know **where** to create the bullet instances. 

Open `Player.tscn` and create a `Node3D` node as a child of the Camera. Name it `bulletSpawn`.  

![Untitled](bulletShooting-bulletSpawn.png)

In 3d mode, move `bulletSpawn` to be in front of the camera. 

> [!note] It might take some experimentation to make it look correct during game play. You may need to change the position a number of times.

![Untitled](bulletShooting-bulletSpawnPosition.png)

Open `Player.gd` and add the code to preload the bullet and configure the spawn point.

> [!warning] Important - the path to the bullet scene and the bulletSpawn point need to be **exactly** as you’ve defined them in your project. If they are named as something else, your code needs to reflect that.

![[bulletShooting-PreloadBullet.png]]

```gdscript
var bulletScene = preload("res://Scenes - Other/bullet.tscn")
var bulletSpawn
```

```
bulletSpawn = get_node("Camera3D/bulletSpawn")
```


Add a new variable to keep track of the ammunition the player is carrying.

Set the value to something appropriate for your project.

![[bulletShooting-Ammo.png]]

```gdscript
var ammo : int = 15
```


Create a new function - `shoot()`- which will run when the shoot input is detected.

> [!note] Change `/Root/Doom` to the name of your root node in the game scene. E.g. `/Root/MainGame`


![Untitled](bulletShooting-RootGame.png)

![[bulletShooting-ScriptShoot.png]]
```gdscript
func shoot ():
    var bullet = bulletScene.instantiate()
    get_node("/root/Doom").add_child(bullet)
    bullet.global_transform = bulletSpawn.global_transform
    bullet.scale = Vector3(0.1,0.1,0.1)
    ammo -= 1
```


Update `_physics_process()` to check to see if the player has pressed the `shoot` input. 

![[bulletShooting-PlayerInput.png]]

```gdscript
if Input.is_action_just_pressed("player_shoot"):
    shoot()
```

Run the game at this stage to test the creation and shooting of bullet instances.


![[commonBlocks#Commit & Push]]