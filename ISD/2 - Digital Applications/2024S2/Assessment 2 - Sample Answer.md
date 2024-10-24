
# Project Overview


## Time Management Overview

> [!important] The timings or details may not be accurate. This is just an example.
> 

![[timeManagementOverview.png]]
**Include Analysis**

For more details, please see [[Assessment 2 - Sample Answer#Work Skills|Work Skills]].

# Code

  

# Data

The player health and enemy health values are managed by the respective scripts - `player.gd`and `enemy.gd`. Both player and enemy instances have scripts attached to them which manages the current health. The players health gets reduced when the player instance collides with enemy instances. The enemy's health is reduced when the player shoots the enemy - this is implemented as when a bullet instance collides with a enemy instance.

**Summary of the health details:**

|                                        | Player                                                  | Enemy                                                    |
| -------------------------------------- | ------------------------------------------------------- | -------------------------------------------------------- |
| Health script                          | `player.gd`                                             | `enemy.gd`                                               |
| variable name                          | `player_health`                                         | `health`                                                 |
| starting value                         | 100                                                     | 100                                                      |
| Damage taken when hit by enemy bullet  | 10                                                      | X                                                        |
| Damage taken when hit by player bullet | X                                                       | 50                                                       |
| Function to take damage                | ![[codeReduceHealth.png]]                    | ![[codeTakeDamage.png]]                     |
| Code which causes damage to be taken   | From `enemy.gd`<br>![[codePlayerTakesDamage.png]] | from `bullet.gd`<br>![[codeEnemyTakesDamage.png]] |
|                                        |                                                         |                                                          |

Due to the fact that individual enemy instance start with health of 100 and each bullet collision reduces the health by 50, this means in this implementation, the enemies take two shots to kill.
Due to the fact that each enemy collision with the player instance reduces the players health by 10, this means that the player can collide with 10 enemies before 'dying' and the game is over.

  

# Development Process

  

# Technical Analysis

  

# Work Skills

