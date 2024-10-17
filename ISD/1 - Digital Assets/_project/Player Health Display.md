
 ![[playerHealthHeartsFull.png]]


  

Hearts for Health Implemented.

  

This is based on this tutorial.

  

[Heart Containers: 3 Ways :: Godot 3 Recipes](https://kidscancode.org/godot_recipes/3.x/ui/heart_containers_3/index.html)

  

Download the Asset library from this page.

  

[https://kenney.nl/assets/platformer-art-deluxe](https://kenney.nl/assets/platformer-art-deluxe)

  

Unzip the file and find the three heart images.

  ![[playerHealthHeartsExtract.png]]


  

Copy these into the Images folder in your project. In the example here, the images are stored in a folder called ************hearts************ however they can be stored anywhere in the project.

  

<aside>

‼️ The path to the images in the code later will need to match!

  

</aside>

  
![[playerHealthHeartsImport.png]]
  

Opening the desired scene, create a VBoxContainer, called `Health`. Create Five (or as many as the game requires) ********TextureRect********s as children of the VBoxContainer.

  ![[playerHealthHeartsNodes.png]]
  

Rename the TextureRects to 1..2..3.. etc. Drag the Heart image onto each of the TextureRects.

Additionally, set the StretchMode to be Keep

  ![[playerHealthHeartsTextures.png]]



  

Attach a script to the `Health` HboxContainer, naming the file `health.gd`. Replace the contents with the code shown.

  

At this stage, nothing will occur if the game is run. The `update_health` function will need to be called by the main game script to update the hearts based on the players health.

  

```python

extends HBoxContainer

  

enum MODES {simple, empty, partial}

  

var heart_full = preload("res://Images/hearts/hud_heartFull.png")

var heart_empty = preload("res://Images/hearts/hud_heartEmpty.png")

var heart_half = preload("res://Images/hearts/hud_heartHalf.png")

  

export (MODES) var mode = MODES.simple

  

func update_health(value):

match mode:

MODES.simple:

update_simple(value)

MODES.empty:

update_empty(value)

MODES.partial:

update_partial(value)

  

func update_simple(value):

for i in get_child_count():

get_child(i).visible = value > i

  

func update_empty(value):

for i in get_child_count():

if value > i:

get_child(i).texture = heart_full

else:

get_child(i).texture = heart_empty

func update_partial(value):

for i in get_child_count():

if value > i * 2 + 1:

get_child(i).texture = heart_full

elif value > i * 2:

get_child(i).texture = heart_half

else:

get_child(i).texture = heart_empty

```

  

********************REMEMBER!!!******************** The paths to the images need to match. Check capitalisations and the **********exact********** path for each of the images.

  ![[playerHealthHeartsPreloadImages.png]]


  

Edit the `[MainGame.gd](http://MainGame.gd)` and add the following code into `_process(delta)`.



> ‼️ The path to the Health and player nodes will depend on your setup. Change the `$HUD/Health` and `$Player` as necessary to fit the specific nodes.


  ![[playerHealthHeartsUpdateHealth.png]]



  

```python

$HUD/Health.update_health($Player.health)

```

  

Make sure the Players health variable is set to `export` in the player script.

  

Set the players health to match the number of hearts you need.

  
![[playerHealthHeartsInit.png]]
  

Run the game!

  ![[playerHealthHeartsExampleFull.gif]]



  

## “Partial” Version

  

The Partial Version of the script uses the half hearts. This could be used if your player health was more than the number of hearts you wanted on screen. For instance, if the player’s health was 10, but only had the space for 5 hearts.

  

To configure the partial version of the health bars, open `[Health.gd](http://Health.gd)` and change the `MODES` to `partial`.

  
![[playerHealthHeartsPartial.png]]


  

Set the players health to an appropriate value and run the game.

  
![[playerHealthHeartsExamplePartial.gif]]
![[commonBlocks#Commit & Push]]