
# Countdown Timer

  

On this page, you'll be shown how to create a simple countdown Timer which updates the screen with the current time.

  

# Interface

  

Create a label node in the scene and note where in the hierarchy you created it. In the case below, the node is called `Countdown` and it's stored under `HUD`.

  ![[newNodeCountdown.png]]

  

That's it for the interface at this stage!

  

# Code

  

In the main Scene, update the `MainGame.gd` code to include two variables at the top:

  

```gdscript
export(int) var countdownMax
var currentTimer
```

  

The `countdownMax` variable is used to store the starting value for the countdown and is set through the Inspector of the main scene

  ![[setCountdownMax.png]]


The currentTimer variable is used to keep track of the current time, which will be reduced by 1 each second.


Next, update the _ready function to first set the currentTimer to the maximum, and update the Label.

  

```gdscript
currentTimer = countdownMax
$HUD/Countdown.text = str(currentTimer)
```


> You will need to change the `$HUD/Countdown` to match where the countdown timer label is in your scene view!!

  

Then you'll create a look which updates the Countdown label, waits a second using the `yield` function, and then reduces the `currentTimer` value by 1


```gdscript

while currentTimer > 0:
	print(currentTimer)
	$HUD/Countdown.text = str(currentTimer)
	yield(get_tree().create_timer(1.0), "timeout")
```

  

When the loop ends, (when `countdownTimer` reaches 0) then you can write the code to do whatever you want. In the case below, it simply outputs Game Over, however you may want to change to another scene.

  

Here is the final code for the `_ready()` function.

  

```gdscript

func _ready():
	#... Existing setup code...
	currentTimer = countdownMax
	$HUD/Countdown.text = str(currentTimer)
	while currentTimer > 0:
		print(currentTimer)
		$HUD/Countdown.text = str(currentTimer)
		yield(get_tree().create_timer(1.0), "timeout")
		currentTimer -= 1
		$HUD/Countdown.text = str(currentTimer)
		print("Game Over")
	#Change to next scene
```

  

# Tutorials

# Animation "Gifs"

To get an animation in an image (like an animated Gif) in your project, you could to use an AnimatedSprite.

[Godot Engine Tutorial Part 9-Sprite Animation - GameFromScratch.com](https://gamefromscratch.com/godot-engine-tutorial-part-9-sprite-animation/)

# Background Colour

[How can I change the default background color](https://godotengine.org/qa/386/how-can-i-change-the-default-background-color)

  ![[commonBlocks#Commit & Push]]