---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 7
---

# Navmesh

Open your first level (level_one.tscn) and add a `NavigationRegion3D` as a child to the root node.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingAddRegion.png]]

Place all the environment nodes to be children of the new `NavigationRegion3D`. 

> [!tip]- What are "Environment nodes"
> "Environment nodes" are any nodes that are static (don't move) nodes. 
This includes objects like:
> - Walls
> - Floor/ground
> - lampposts
> 
> In short, anything that the player or enemies will have to move around or on.


Do **not** move the player node

After moving the nodes, your scene hierarchy should look similar to this.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingMoveEnvironment.png]]

Select the NavigationRegion3D and add a new NavigationMesh in the inspector.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingNewNavMesh.png]]

Click `Bake NavigationMesh` in the scene toolbar.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingBakeNavMesh.png]]

After Baking the navmesh you will see that a highlight will appear. This highlighted area indicates where the enemies are allowed to move in and around. You'll also notice that around your environment meshes, such as the walls, the navmesh is not traversable in this area, meaning that the enemies cannot move into that space.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingNavMesh.png]]

> [!tip]- Navmesh Modifications
> Depending on your environment, and player settings, the default navmesh may not be suitable. If you've changed the size of your enemy node, you'll need match its setting in the navmesh.
> ![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingNavMeshMods.png]]

# Attach Script

At this stage the first level scene doesn't have a script. Attach one!
This script will (at this stage) update any enemy nodes in the game where the player is, so they can track towards it.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingAttachScript.png]]

Remove the default functions, and add a variable that will store the connection to the player.

> [!Note] If you named your Player node differently, or it's not stored as a direct child of the root node, you will need modify the $Player code to match your project.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingSetPlayer.png]]

```gdscript
@onready var player = $Player
```

Add a `_physics_process(delta)` function. In this function, add the following code which:
- Finds all nodes in the scene tagged as "enemy" as a group.
- Calls the `update_target_location` function on each node found
- Sends the players position in the environment as an argument to the `update_target_location` function call.

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingSendPlayersLocation.png]]

```gdscript
func _physics_process(delta):
	get_tree().call_group("enemy", "update_target_location", player.global_transform.origin)
```

# Add a Enemy

Add a enemy node into your game (as a child of the root node **not** under NavigationRegion3D).

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingAddEnemy.png]]

# Run the Game

Finally, run the game and watch the enemy node/s try and track you!

![[ISD/2 - Digital Applications/_topics/tutorials/images/pathfindingFinal.gif]]
# Save The Scene

Save the scene.

![[commonBlocks#Commit & Push]]

# Enemy's focus

Using the steps above, the enemy will end up aiming towards the closest position on the navmesh to the player. Effectively, this means the enemies will aim down towards the player's feet.

![pathfindingEnemyFaceDown](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/pathfindingEnemyFaceDown.png)


This may not be the intended outcome, as the enemy will fire projectiles in that direction. 

To change the enemy's direction, the `look_at` command needs to point to the player, not the position on the navmesh.

To fix this, open `enemy.gd`, and create a new global variable named `root_node`.

![pathfindingRootNodeVariable](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/pathfindingRootNodeVariable.png)

```gdscript
var root_node
```

Create (or edit) the `_ready()` function to set the `root_node` variable to the scene's parent node.

![pathfindingEnemyReadyFunction](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/pathfindingEnemyReadyFunction.png)

> [!tip] This may need to be modified to match the exact specifications of your project.

Update the `_physics_process()` function to find the Player node's position and update the `look_at` command.

![pathfindingLookAtPlayer](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/pathfindingLookAtPlayer.png)


Your Enemy objects should now face the exact position of the player.

![pathfindingLookingAtPlayer](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/pathfindingLookingAtPlayer.png)

![[commonBlocks#Commit & Push]]

