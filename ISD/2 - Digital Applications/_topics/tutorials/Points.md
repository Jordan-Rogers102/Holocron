---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 9
---

# Global Script

> [!tip]- Global script
> You may find that you need to create a new script called `Global.gd` if not already created.. This script is not attached to any node, but will be loaded when the game runs and continue running in the background.
> ![[pointsGlobalScript.png]]

Open `Global.gd`. Replace the contents of the file with this code.

![[pointsGlobalCurrentScore.png]]

```gdscript
extends Node

var current_score = 0
```

Save the File.

In Project Settings (Project → Project Settings). Click on the AutoLoad tab. Browse to the `Global.gd` and enter the Node Name as `Global`.

![[pointsSetAutoLoad.png]]

End Result

Click Close.

# Pickup Item

> [!tip]- The pickup item can be any object you wish. 
> It could be a simple cube or cylinder or a complex object that you’ve imported from 3D modelling software such as Blender. Regardless of the object itself, the object needs to be saved as it’s own Scene. 

For this example, create a new scene, simply with a cylinder object (`CSGCylinder3d`).  Save the file as `Pickup.tscn`. 

![[pickupCylinder.png]]

Create child nodes of the original object to include a mesh that the player can collide with. Add an `Area3D` and then a `CollisionShape3D` child nodes. With the `CollisionShape3D` node selected, set a collision shape as a `CylinderShape3D` to match the mesh.

![[pickupCollisionArea.png]]

Right Click on the Pickup node and attach a script, named `Pickup.gd`. Save the script. There is no need to change the code at this stage.

![[pickupDefaultScript.png]]


Select the `Area3D` node, and switch to the Node tab.

![[pickupSelectNodeTab.png]]

Double click on the Body Entered signal. Make sure the Pickup node is selected and click Connect.

![[pickupConnectSignal.png]]


Enter the following code for the `_on_area_3d_body_entered(body)` function.

This code check to see if the object that collides with the pickup item is the player. If so, it will add 10 points to the `current_score` variable in the Global script.

Then it deletes the pickup item.

![[pickupOnAreaEntered.png]]

```gdscript
if (body.name == "Player"):
	Global.current_score += 10
	queue_free()
```

Save the Scene.



# Place pickup Items

Open the level one scene and place pickup items in your scene.

> [!tip] Remember that the pickup items need to be children of NavigationRegion3D! Don't forget to then re-bake the navmesh.

![[pickupAddInstances.png]]

![[commonBlocks#Commit & Push]]

# Displaying the score

Open the Player scene, and make a child node of the `Camera3D`. The node needs to be a label. Name the label `playerScore`.

![[pickupCameraAddLabel.png]]

![[pickupCameraRenameLabel.png]]

> [!note] You can use HBoxes, VBoxes and other methods to place the score label where you wish it to go. This is just a quick example.

Open the Player script and look for the `_physics_process()` function.

Add the following line of code at the end of the function.

Every frame refresh, this code will take the current_score value and update the playerScore label.

![[pickupUpdateLabel.png]]

```gdscript
$Camera3D/playerScore.text = str(Global.current_score)
```

![[commonBlocks#Commit & Push]]

# Expanding the Points Mechanic
Now that you know how to have items give the player points, you can expand it to different objects in the game. Explore the possibilities!

