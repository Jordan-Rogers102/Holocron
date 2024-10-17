
## Win & Lose Conditions

The Win and Lose conditions refer to the state of gameplay to determine whether the player “wins” the game or “loses” the game. Those states are determined by the game itself and what occurs after is up to the developer.

Some examples could be:

| Win Condition | Lose Condition |
| -- | --|
| All enemies are killed | The player’s health reaches 0. |
| The door at the end of the level is opened | The player runs out of ammunition. |
| The player survives the night | |
| etc. | etc.|

In our clone of space invaders, the following conditions exist (at a minimum)

| Win Condition/s | Lose Condition/s |
| --- | --- |
| All enemies are defeated | The timer reaches 0. |
| | The player’s health reaches 0. |

  

## Win Condition

  

Expand each of the following to implement the different conditions.

  

### All Enemies are Defeated

  

Open `MainGame.tscn`, and click on the “Open in Editor” button next to one of the individual enemy nodes.

  ![[winLoseEnemiesDefeated.png]]


  

This opens the original scene to edit. All of the individual enemies in the game are based on this one scene.

  

With the root node selected, click on the Node tab, then click on Groups. Enter “enemy” and click Add.

  ![[winLoseAddGroup.png]]



Save the scene. This adds this tag to each individual enemy.

  

Return to Main Game.

  

Open `MainGame.gd`, and in the `_process()` function, check if there are no more nodes with the tag enemy left. If there are none, then go to the Win Scene.

  

```gdscript

func _process(delta):
	$HUD/CurrentScore.text = str(GlobalVariables.scoringInformation["currentScore"])
	if get_tree().get_nodes_in_group("enemy").size() == 0:
		get_tree().change_scene("res://WinScene.tscn")

```

  

Change `res://WinScene.tscn` to link to the Win Scene in your project.

  

## Lose Condition

  

Expand each of the following to implement the different conditions.

  

### The Timer Reaches 0

  

To implement this condition check, open the MainGame.gd script and look in the _ready() function.

  ![[winLoseTimerReachesZero.png]]  

If Line 17 is reached, it outputs `Game Over` to the console, which means the timer has reached 0. This is where the code will need to go to make it perform a function. Luckily the condition check has already been performed!

  

Create a New Scene through the `Scene` Menu

  ![[winLoseNewScene.png]]


  

Choose Node2D in the hierarchy tab to start the scene, and then Right Click on the Node2D and choose `Add Child Node`.

  ![[winLoseAddChildNode.png]]  

Search for, and add, a VBoxContainer

  ![[winLoseAddVBox.png]]



  

Rename the VboxContainer as Layout. Right click on that, and choose Add Child Node.

  ![[winLoseRenameVBox.png]]


  

This time, search for and add a Label

  ![[winLoseAddLabel.png]]



  

Rename the Label as Heading, and then change the text attribute to “You Lost” or anything else appropriate.

  ![[winLoseConfigureLabel.png]]


Now add a button as a child of the VboxContainer called Layout.

  ![[winLoseLayout.png]]


  

Change the text to `Return to the Main Menu,` or anything else appropriate.

  ![[winLoseButtonReturn.png]]

Right click on the button in the hierarchy and choose `Attach Script`.

  ![[winLoseAttachScript.png]]


Don’t change any of the defaults and just click Create.
![[winLoseCreateScript.png]]



  

With the button selected, switch to the Node tab as shown.

  ![[winLoseNodeTab.png]]

Double click on the `pressed` signal.

![[winLosePressedSignal.png]]


  

Don’t change anything here - just click `Connect`.

  ![[winLosePressConnect.png]]



  

Change the script to the code shown below.

  

```gdscript
func _on_Button_pressed():
	get_tree().change_scene("res://Menu/Menu.tscn")
```

  

❓ Note that the `res://Menu/Menu.tscn` may need to be modified to match your project. It needs to be the path to *your* main menu scene.


![[winLoseChangeScene.png]]


  

Save the Scene.
![[winLoseSaveScene.png]]
  

  

Go back to MainMenu.gd and after the print("Game Over") code, you will need to add the following:

  

```gdscript
get_tree().change_scene("res://LoseScene.tscn")
```

  


❓ Remember the scene linked will need to match *your* project. Change `res://LoseScene.tscn` to whatever you need to link it to the scene you just created.

  

  

### The Player’s Health Reaches 0.

  ![[commonBlocks#Commit & Push]]