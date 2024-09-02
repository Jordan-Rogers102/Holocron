---
author: Ryan Cather
date: 2024-06-09
priority: 2
order: 13
---
> [!info] **Lose conditions** in game development define the specific criteria that, when met, result in the player losing the game. They provide a sense of challenge and stakes to the gameplay and encourage players to avoid making mistakes.
> 
> **Common Lose Conditions:**
> 
> - **Character death:** The player's character dies, either from enemy attacks, environmental hazards, or other causes.
> - **Game over:** The player fails to complete a critical objective or task, such as reaching a checkpoint or defeating a boss.
> - **Time limit:** The player runs out of time to complete a level or objective.
> - **Resource depletion:** The player runs out of essential resources, such as health, ammo, or money.
> - **Environmental hazards:** The player is killed by environmental hazards, such as lava, spikes, or falling objects.
> - **Enemy overwhelming:** The player is defeated by a large number of enemies or an overly powerful enemy.
> - **Puzzle failure:** The player fails to solve a puzzle or complete a challenge within a certain number of attempts.
> Google Gemini




There could be several ways for the player to lose. This page will show some common ones.

# Run out of time

No timer is currently implemented in the game, however, this is easy to include. 

## Option 1: Pure Code
One of the easiest methods is a similar approach to how it was implemented in Space Invaders, through a `while` loop in the main game script.

![countDownTimer](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/countDownTimer.png)

```gdscript
var current_timer = 50
 
func _ready():
	$HUD/Countdown.text = str(current_timer)
	while current_timer > 0:
		await get_tree().create_timer(1).timeout
		current_timer = current_timer - 1
		$HUD/Countdown.text = str(current_timer)
	# now the timer is 0. Player has lost.
	get_tree().change_scene_to_file("res://Game/LoseScene.tscn")
```

> [!tip] Note!
> - In Godot 4, `await` is used instead of `yield` from Godot 3.x
> - This script assumes several things:
> 1. The node `$HUD/Countdown` exists. Change this to match your project - linking it to a Label on the HUD for the user. Or remove/comment those lines, and
> 2. You have a scene called `res://Game/LoseScene.tscn`. Change this to the scene you wish to load if the player runs out of time.


## Option 2: A `Timer` node

First, add a `Timer` child node to the main game scene.

![countdownTimerNode](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/countdownTimerNode.png)

Set the `Wait Time` setting to however many seconds you wish the game to run for. The timer will start at that time, and count down.
Set the `One Shot` and `Autostart` settings to **On**.

![countdownTimerInspector](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/countdownTimerInspector.png)


Change to the Node tab for the Timer and double click on the `timeout()` signal. Accept the default settings and click Connect.

![countTimerSignalSettings](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/countTimerSignalSettings.png)


This will create the function for you. Add the code to change to the Lose Scene once the timer has finished. You may also wish to add code to update the Countdown Timer on the HUD for the player to see.

![countdownTimerCode](ISD/2%20-%20Digital%20Applications/_topics/tutorials/images/countdownTimerCode.png)

```gdscript
func _process(delta):
	var timer_to_display = int($Timer.time_left) 
	$HUD/Countdown.text = str(timer_to_display)


func _on_timer_timeout():
	get_tree().change_scene_to_file("res://Game/LoseScene.tscn")
```

> [!tip] The code shown in `_process()`  has to convert the data twice. The `time_left` value is a `float` which means it's a decimal point value. The player doesn't need that level of detail (e.g. 4.9482740237 seconds left), so the first step is to *cast* it as an integer (whole number). To display it in the label `Countdown`, the data must be a string, so the integer `timer_to_display` is then cast as a string. 



# No Health

This is covered in [Player Health](ISD/2%20-%20Digital%20Applications/_topics/tutorials/Player%20Health.md).

