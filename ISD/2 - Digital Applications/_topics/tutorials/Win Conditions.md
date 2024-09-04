---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 13
---
> [!info]- Goal - How does the player win the game?
> Certain conditions need to be met before the player can win. These may be 
> Every game has different win conditions, sometimes multiple ways.


>[!info] **Win conditions** in games define the specific objectives or criteria that players must meet in order to achieve victory. They provide a sense of purpose and direction for players, and add stakes to the gameplay.
>
>Example Win Conditions
>**Simplified Win Conditions for Game Development in Godot:**
>
> - **Reach the end:** Get to the final level or destination.
> - **Complete tasks:** Do what the game tells you to do, like collect items or defeat enemies.
>- **Get points:** Score enough points to win.
> - **Solve puzzles:** Figure out how to overcome obstacles or challenges.
> - **Control the map:** Capture areas or defeat enemies to gain control.
> - **Collect resources:** Gather enough money, items, or other resources to win.
> - **Level up:** Make your characters stronger or gain new abilities.
> - **Beat the bad guys:** Defeat all the enemies, including the final boss.
> - **Race against time:** Complete objectives before the timer runs out.
> 
> **Special Win Conditions:**
> 
> - **Different endings:** Win the game in different ways based on your choices.
> - **Endless challenges:** Keep playing and getting better, with no end in sight.
> - **Team up:** Work with other players to achieve victory.
> - **Lose conditions:** If you fail, you might lose your progress or even the game.



# Kill All Enemies

Different approaches could be taken for this win condition. One of the easiest ones is to keep playing the game until the number of instance in within the `enemy` group reaches 0.

Currently, each enemy instance has been assigned to the `enemy` group. 

> [!tip] If you have a number of differnet enemy types with a different group (e.g. `enemy` and `bossenemy`), then create a new group for all enemies (such as `all_enemies`) and apply this section to the new group name.

To check if there are nodes in group "enemy" above 0 in Godot 4, you can use the following code:

```gdscript
if get_tree().get_nodes_in_group("enemy").size() > 0:
    # There is at least one node in the "enemy" group
else:
    # There are no nodes in the "enemy" group
```

> [!info]- Here's a breakdown of the code:
> 
> - `get_node_count("enemy")` returns the number of nodes in the "enemy" group.
> - The `if` statement checks if the number of nodes in the "enemy" group is greater than 0.
> - If the condition is true, it means there is at least one node in the "enemy" group.
> - If the condition is false, it means there are no nodes in the "enemy" group.

You can use this code to check if there are any enemies remaining in a level, or to trigger events based on the number of enemies present.

Here's an example of how you could use this code in a game:

```gdscript
func _process(delta):
	if get_tree().get_nodes_in_group("enemy").size() == 0:
		# All enemies have been defeated, so proceed to the next level
		get_tree().change_scene("next_level")
```

In this example, the `_process` function checks every frame if there are any nodes in the "enemy" group. If there are no nodes in the group, it means all enemies have been defeated and the game can proceed to the next level.

This code could be placed on the script for the player or the level. Whichever you choose, make sure that the `if` code block above is put in the `_process` function. Don't create a second `_process()` function! Look for an existing `_process()` function and add it there.



