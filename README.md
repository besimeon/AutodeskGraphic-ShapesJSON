# AutodeskGraphic-ShapesJSON
This script was developed with the goal of automating the pipeline that creates assets from Autodesk Graphic for use in an HTML5 game using the Phaser2 engine.

Phaser2 requires x & y parameters during the asset loading process to position a given asset in world space, so the JSON contains x, y, width, and height dimensions.  In order to keep the positioning of said assets consistent with their positioning in the Autodesk Graphic scene, the JSON lists all data as percentages of the Autodesk Graphic canvas dimensions.

# Installation

Copy the following file ```exportShapesJSON``` to the following directory ```/Users/YOUR-USERNAME/Library/Containers/com.indeeo.idraw/Data/Library/Application Support/iDraw/Plug-ins```

# Running the script

Start Autodesk Graphic and open the file containing the shapes in question & navigate to: ```Plugins > exportShapesJSON ```

At this point the script should run and create a create a prompt containing JSON data.

## Using the JSON data

To use the JSON data in Phaser:

1.  Select a portion of the JSON data in the prompt created by the script.
2.  Press "Command + a" to select all of the data.
NOTE:  It DOESN'T MATTER if all of the data is VISIBLE on-screen.  If you press "Command + a", all of the data WILL BE COPIED.
3.  Press "Command + c" to copy the selected data.
4.  In your editor of choice, create a new file for the JSON data & press "Command + v" to paste the JSON data.
NOTE:  Or, you could paste the JSON data directly into your Phaser project if you prefer.
