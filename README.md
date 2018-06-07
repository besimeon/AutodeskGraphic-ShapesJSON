# AutodeskGraphic-ShapesJSON
This script was developed with the goal of automating the pipeline that creates assets from Autodesk Graphic for use in an HTML5 game using the Phaser2 engine.

Phaser2 requires x & y parameters during the asset loading process to position a given asset in world space, so the JSON contains x, y, width, and height dimensions.  In order to keep the positioning of said assets consistent with their positioning in the Autodesk Graphic scene, the JSON lists all data as percentages of the Autodesk Graphic canvas dimensions.


# Installation

Copy the following files: ```exportShapesJSON-activeLayer.idplugin``` ```exportShapesJSON-selectedShapes```to the following directory ```/Users/YOUR-USERNAME/Library/Containers/com.indeeo.idraw/Data/Library/Application Support/iDraw/Plug-ins```

# Running the script

1. Start Autodesk Graphic and open the file containing the shapes in question.

*NOTE: Be mindful of shape names, if they are important to your use-case.*
*If a shape's name is left assigned its default value of "Shape", the script will RENAME the shape to shape-[index].*
*This renaming functionality is a workaround implemented to avoid a bug where the script detects a null value for the shape's name when said shape is left assigned its default value of "Shape".*

### Option 1: For all shapes in a given layer: 
2a. Make sure all shapes needing JSON Data exported are in the same layer.  
3a. navigate to: ```Plugins > exportShapesJSON-activeLayer```

### Option 2: For all selected shapes:
2b. Select all shapes needing JSON Data exported.  
3b. navigate to: ```Plugins > exportShapesJSON-selectedShapes```

At this point the script should run and create a create a prompt containing JSON data.

## Using the JSON data in Phaser:

### PART 1: create the JSON:
1.  Select a portion of the JSON data in the prompt created by the script.
2.  Press "Command + a" to select all of the data.

*NOTE:  It DOESN'T MATTER if all of the data is VISIBLE on-screen.  If you press "Command + a", all of the data WILL BE COPIED.*

3.  Press "Command + c" to copy the selected data.
4.  In your editor of choice, create a new file for the JSON data & press "Command + v" to paste the JSON data.  
5.  Encapsulate the entire set of pasted data in {}'s, indent accordingly, and assign a variable to the JSON data.  
6.	Save as a JSON file. 

*NOTE:  Or, you could paste the JSON data wherever you would place the JSON data in your project.*

### PART 2: using the data during object creation:
1. add link to the JSON file in your main Phaser project located preceeding any code accessing it.  
2. in your Preload() funciton, iterate through yourJSONvariable.shapes during game.load.image to create the images. 

``` Example using buildingsData as my JSONvariable name:

	for (var i = 0; i<buildingsData.shapes.length; i++){
		var fileName = "assets/" +buildingsData.shapes[i].name+ ".png";
		game.load.image(buildingsData.shapes[i].name, fileName);
	}
```

3.  in your Create() function, iterate through yourJSONvariable.shapes when placing objects using xPers, yPers, and yourJSONvariable.shapes[index].name. Create a variable for the ratio of height of the world in Phaser to the height of canvas in AutoDesk Graphic.  Multiply by this variable when scaling each object.  

``` Example using buildingsData as my JSONvariable name, 500 for my canvas height in Autodesk Graphic, and gameHeight containing my game height in Phaser:
	
	// ratio of height of Phaser game world and height of AD Graphic canvas:
	var canvasHeightRatio = gameHeight / 500; 
	// iterate through buildingsData, which contains the JSON created by the AD script:
	for (var i = 0; i<buildingsData.shapes.length; i++){
		// using xPers & yPers when setting position:
	    var building = buildings.create((game.world.width * buildingsData.shapes[i].xPers), (game.world.height * buildingsData.shapes[i].yPers), buildingsData.shapes[i].name);
	    // multiplying by height ratio variable when setting scale:
	    building.scale.setTo(1*canvasHeightRatio, 1*canvasHeightRatio);
	}
```

*NOTE:  these instructions assume both the AD Graphic file and the Phaser world dimensions are the same aspect ratio.  If you are using different aspect ratios, you will need to create separate canvasWidthRatio and canvasHeightRatio variables for use when scaling objects.*  


# ENJOY!

And there you have it.  You now have shapes placed and scaled in Phaser equivelent to their placement and scale in Autodesk Graphic.  

For feedback, contact me here in github or goto blakesimeon.com.


# Future updates in the works:

-exportAtlasJSON script for use-cases involving sprite atlases in Phaser.  
