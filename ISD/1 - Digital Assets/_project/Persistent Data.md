In this tutorial, you’ll be shown how to save and load the `scoringInformation` dictionary.

  
<aside>

❓ In this tutorial, only a small amount of data will be saved and loaded, so not a lot of focus on serialisation is done. However if the game requires saving more complex data, you will need to ensure this is done.

  

</aside>

  

Open [Global.g](http://Global.gs)d and create a new global variable which sets the save file.

  ![[persistentDataSaveFile.png]]

```gdscript

var saveFile = "user://save.dat"

```

  

### Saving the data

  

To ensure it’s saved when it is updated, the saving of high score data can be done in the Win Scene.


Open `WinScene.gd` and create a new function called `saveData()`.

  
![[persistentDataWinSceneFunc.png]]


```python

func saveData():

```

  

Update `saveData()` to attempt to access the file name specified in `Global.gd` called `saveFile`. If there is no issues with that file, it will write the scoringInformation dictionary to the file and close the connection.

  
![[persistentDataSaveDataFuncComplete.png]]


```gdscript

func saveData():
	var file = File.new()
	var error = file.open(GlobalVariables.saveFile, file.WRITE)
	if error == OK:
		file.store_var(GlobalVariables.scoringInformation)
		file.close()
		print("!!Data Saved!!")
	else :
		print("!!Data Not Saved!!")
```

  

Lastly, update the `_ready()` function to call the `saveData()` function.

  ![[persistentDataSaveDataFuncCall.png]]


  

### Loading the Data

  

Open the main menu and look at the script for the scene - `Menu.gd`.

  

Update the `_ready()` function to load (or attempt to load) the saved data.

  

This code checks to see if the file exists first - applications don’t like attempting to open files that don’t exist.

  

If the file is there, it replaces the `scoringInformation` data that’s coded by default with the loaded data. If there is any error, it just leaves the default values.

  ![[persistentDataLoad.png]]



  

- Code

```python

var file = File.new()

if file.file_exists(GlobalVariables.saveFile):

var error = file.open(GlobalVariables.saveFile, File.READ)

if error == OK:

var player_data = file.get_var()

file.close()

GlobalVariables.scoringInformation = player_data

```

  
  ![[commonBlocks#Commit & Push]]

  

## Bug or Feature?

  

There’s a bug with the saving and loading of `scoringInformation`. Did you notice? It’s got to do with currentScore - it’s not resetting correctly and is saving the current score in the save file.
