# Architectural Cartograms
**_Convert 2D architectural projections into animated cartograms_**

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/demo_.gif" width="400"> <img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/elev_demo.gif" width="400">

### Prerequisites

- [Rhino 6](https://www.rhino3d.com/6)
- [GHPython](https://www.food4rhino.com/app/ghpython)
- [Kangaroo Physics](https://www.food4rhino.com/app/kangaroo-physics)
- [Human UI](https://www.food4rhino.com/app/human-ui)

### Files

- `model.gh` use this file to control deformation of 2D elements by material and record deformation process through screenshots.

- `base.3dm`: build off of this 3dm file as layer structure is already setup. 


### Get started & method description
Download this repository by clicking on the green button on the rigth side of this page "Clone or download". The only files that you will need are the .3dm and .gh ones. 
This adapated cartogram method works only with **2D closed polyline** geometry. Make sure that the drawings you are making use only closed polylines and avoid any misaligned polyline vertices or badly overlapping edges. The method uses a physics-based approach to deform each polyline to reach target areas. There are several other constraints in place to minimize wierd deformations in place but you may disergard those parts of the .gh graph.


### Implementation

#### 2D drawing setup
To setup your rhino file create your 2D drawing with only closed polylines (the `curve boolean` tool in Rhino is a good method to make sure the drawing is made of closed polylines) and assign each polyline to a material layer (see following section).

#### Set anchors
In case needed, you can set `anchors`, points that need to be located on top of certain polyline vertices to lock them in place. No deformation will ever move these around. You can do so by selecting the layer `anchors_` and placing points on the desired vertices. These will be loaded automatically by the gh file and visualized with red dots. 

#### Layers by material
In the base.3dm file there is already a layer structure that you can edit for your own purposes. Material layers (for now named with placeholders "m1", "m2", "m3"... ) are grouped under a master layer. In the file you will see two master layers `MATERIALS_elevation` and `MATERIALS_perspective` that were used for testing. Use either of these to get started. NOTE: the master layer name, the material sub-layer names in Rhino and the names of the material multiplier sliders in GH need to be consistent. If you change the names in Rhino please update accordingly the name in GH. For now you will see extra sliders that can be used in case you add more materials (more layers) in Rhino. 

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/rhino_layers2.PNG" width="250"> <img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/material_sliders_andLoading.PNG" width="300"> 

#### Load geometry in gh
Once the geometry is setup and divided in the different layers go the gh file and update the panel `GROUP LAYER NAME` with the your master layer name in case you created a new master layer or changed one of the existing two. Then hit the `RESET!` button to update the series of Python nodes that automatically load all geometry by material and assign the related embodied energy multiplier values. Your polylines will be filled with an orange color, at their center you should see the value "1" in black and below the name of assigned material in grey. Check that all polylines have been filled in orange, if there are "white spots" that means some geometry is either missing or has not been assigned to any layer. 

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/layer_reset_button.PNG" width="400">
"reset button image"

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/img_preview.PNG" width="250">
"image preview"

#### Run the deformation sim
Once geometry is all setup you can navigate to the file's main controllers which include the embodied energy multiplier sliders per material, a button to run Kangaroo and a series of controllers for automatic screenshot capturing. 

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/main_control_sliders.PNG" width="400">
"main controllers" <br />


Now follow these steps:
1. Run the Kangaroo simulation by hitting the `runSim` button. Now Kangaroo is active.
2. Slowly change one multiplier slider at a time until you reach the desired level relative embodied energy difference. 

This is a delicate process as the deformation could fail or get very wierd if there are issues with the geometry (see points above), if the multipliers are too high (or too low), or because of other causes. These steps will have to be repeated iteratively by changing order of material deformation or redrawing certain parts of the drawing. Because of this you can easily reset every multiplier slider to the value of 1.0 (no deformation) by hitting the `reset to 1.0` button.
Advise: start with few geometry, test the deformations, go back to Rhino, add more geometry, test the deformation etc. 

#### Save out frames to record deformation process
Once you reached a desired deformation state you can record the deformation process through automated screenshot capturing. 

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/screenshot_controls.PNG" width="400">
"screenshot capturing controllers"

To do so before going through step 1 and 2: 
1. create a `floating viewport` in Rhino, 
2. adjust the size (resolution) of the viewport in the properties panel, 
3. name and save the view,
4. in gh fill in the panel "output folder" (this will create a folder within a folder called "frames" in the same directory of your gh file)
5. type in the name of the view you saved in the "viewport name" panel
6. set corresponding resolution in the two remaining panels (if resolution does not match the rhino ones, these will override the Rhino ones).


### Examples

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/Gif-2019-07-19-16-07-51.gif" width="400">
*Deformation of 2D perspective*

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/elev_demo.gif" width="400">
*Deformation of elevation drawing*
