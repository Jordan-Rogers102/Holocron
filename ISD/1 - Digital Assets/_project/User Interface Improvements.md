
Goals

  

Create the Main Menu Interface.

  

<aside>

<img src="https://www.notion.so/icons/list_orange.svg" alt="https://www.notion.so/icons/list_orange.svg" width="40px" /> $\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Table of Contents}}$

  

</aside>

  

# Tutorials

  

## Main Menu

  

### **Part 1 - Menu Setup**

  

![https://youtu.be/DyaKLWr502M](https://youtu.be/DyaKLWr502M)

  

In this video, you'll see how to configure the project window size and colour as well as start the layout of the menu.

  

You'll see how to add images into the scene as well as a label, with a brief introduction on how to layout these items.

  

### **Part 2**

  

![https://youtu.be/CBA3sxDbgog](https://youtu.be/CBA3sxDbgog)

  

In this video, you'll create the "AppInfo" section of the title screen, including the version number, developer and high score information.

  

You'll also learn briefly about "Size Flags" to layout the App Info section, expanding labels to fill additional space on screen.

  

### **Part 3**

  

![https://youtu.be/PxyPHJmNflI](https://youtu.be/PxyPHJmNflI)

  

This video focuses on the Buttons the title scene. You'll see how to create the buttons, and modify the fonts to match the title font, and then change the font of all the buttons to a new font.

  

## Buttons Functionality

  

![https://youtu.be/QH_5xVreQ-w](https://youtu.be/QH_5xVreQ-w)

  

- Code - TitleScene.gd

```python

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

- Code - ButtonScript.gd

```python

extends Button

export(String) var scene_to_load

```

- Code - MainGame.gd

```python

extends Control

# Called when the node enters the scene tree for the first time.

func _ready():

for button in $HUD.get_children():

button.connect("pressed", self, "_on_Button_pressed", [button.scene_to_load])

func _on_Button_pressed(scene_to_load):

print("Changing Scene...")

print(scene_to_load)

get_tree().change_scene(scene_to_load)

```

  

In this video, you're shown one way of changing between scenes.

  

You're shown a number of aspects to the process:

  

- Creating the new Scene

- Creating scripts for the buttons to store the scene names

- Reusing the script between buttons and scenes

- Writing a script to manage all the buttons in the scene

- Parts of programming, such as loops, functions and arrays.

  ![[commonBlocks#Commit & Push]]