
# Buttons Functionality


![https://youtu.be/QH_5xVreQ-w](https://youtu.be/QH_5xVreQ-w)

  

In this video, you're shown one way of changing between scenes.


You're shown a number of aspects to the process:
  

- Creating the new Scene

- Creating scripts for the buttons to store the scene names

- Reusing the script between buttons and scenes

- Writing a script to manage all the buttons in the scene

- Parts of programming, such as loops, functions and arrays.

  

The code used in this video is:


## TitleScene.gd

```gdscript

extends Control

# Called when the node enters the scene tree for the first time.

func _ready():
	for button in $"Menu/Menu Buttons/Buttons".get_children():
	button.connect("pressed", self, "_on_Button_pressed", [button.scene_to_load])

func _on_Button_pressed(scene_to_load):
	print("Changing Scene...")
	print(scene_to_load)
	get_tree().change_scene(scene_to_load)

```

## ButtonScript.gd

```gdscript

extends Button

export(String) var scene_to_load

```

## MainGame.gd

```gdscript

extends Control

# Called when the node enters the scene tree for the first time.

func _ready():
	for button in $"Layout/Main/Buttons/GameScenes".get_children():
	button.connect("pressed", self, "_on_Button_Pressed", [button.scene_to_load])

func _on_Button_Pressed(scene_to_load):
	print(scene_to_load)
	get_tree().change_scene(scene_to_load)
```

  ![[commonBlocks#Commit & Push]]