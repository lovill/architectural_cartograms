# Architectural Cartograms
**_Convert architectural projections into animated cartograms_**

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/demo_.gif" width="400">

### Prerequisites

- [Rhino 6](https://www.rhino3d.com/6)
- [GHPython](https://www.food4rhino.com/app/ghpython)
- [Kangaroo Physics](https://www.food4rhino.com/app/kangaroo-physics)
- [Human UI](https://www.food4rhino.com/app/human-ui)

### Files

- `model.gh`: This is the Grasshopper file used to run .

- `base.3dm`: Build off of this 3dm file as layer structure is already setup. 

### Get started & Intro
Download this repository by clicking on the green button on the rigth side of this page "Clone or download". The only files that you will need are the .3dm and .gh ones. 
This adapated cartogram method works only with **2D closed polyline** geometry. Make sure that the drawings you are making use only closed polylines and avoid any misaligned polyline vertices or badly overlapping edges. The method uses a physics-based approach to deform each polyline to reach target areas. There are several other constraints in place to minimize wierd deformations in place but you may disergard those parts of the .gh graph.

#### 2D drawing setup
To setup your rhino file create your 2D drawing with only closed polylines (the `curve boolean` tool in Rhino is a good method to make sure the drawing is made of closed polylines) and assign each polyline to a material layer (see following section).


#### Layers by material
In the base.3dm file there is already a layer structure that you can edit for your own purposes. Material layers (for now named with placeholders "m1", "m2", "m3"... ) are grouped under a master layer. In the file you will see two master layers `MATERIALS_elevation` and `MATERIALS_perspective` that were used for testing. Use either of these to get started. 

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/rhino_layers.PNG" width="400">


`archi_cartogram.gh` and `base.3dm` and the `py` directory and keep all items in a local directory of your choice. Run Rhino file, launch Grasshopper, load GH file and explore procedural stacking.



Move/add/remove/rotate manually the first layer units (highlighted in red) and/or change all relevant input parameters as described in GH file. 



### Examples

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/Gif-2019-07-19-16-07-51.gif" width="400">
*image_caption*

<img src="https://github.com/lovill/architectural_cartograms/blob/develop/media/elev_demo.gif" width="400">
*image_caption*
