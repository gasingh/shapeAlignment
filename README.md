# 3D Shape Registration & Automated Alignment
**Mesh Alignments for Rhino3D**

<img src="https://raw.githubusercontent.com/gasingh/shapeAlignment/main/ViewCapture20240531_043415%20-%20Copy.jpg" width="900"> <br>
 <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view7_octopusDualRun5_optimal2_frame46.png" width="900"><br>
 <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view7_octopusDualRun2_optimal_frame30.png" width="900"><br>

_The envisaged usefulness of this tool is for use in the Architecture, Engineering and Construction Industry, for purposes of mesh geometry verification and the need for precise mesh to mesh alignments, esp. in cases of geometries with unknown generation history._

`#machine-learning` `#statistics` `#linear-algebra` `#applied-maths` `#3d` `#geometry`

## Toolkit Purpose
- This is a native IronPython implementation of mesh alignment functionalities for **Rhino3D**, from scratch.
- The aim is to be able to be able to provide functionalities such as **mesh to mesh alignments**, and **mesh shape verification**.

## Use Cases
- **AEC Industry**: (Facade Components and manufacturable assemblies) Very useful to estimate similarity of facade geometries, and shape verification.
  - Accurate comparison of 3d Meshes.
  - Automated alignment of shape parts in 3d space.
- **Archeology**: Fields such as archology where physical artifacts are often scanned and kept in digital repositories, could also benefit from such a tool. 
    
## Demonstration of Mesh Alignments inside Rhino 3D on various datasets
  
### 1. Stanford Bunny
  Mesh: Decimated Stanford Bunny with 178 faces, 95 vertices.
  
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240530_icp_view1.gif" width="800" /> </br>
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240530_icp_view2.gif" width="800" /> </br>
  
### 2. Octopus
  Mesh: High Resolution Octopus with 3436 faces, 1752 vertices.
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view6_octopus_rec4_final.gif" width="800" /> </br>
  The animation below shows the central octopus aligning to the two side octopuses in different poses. <br>
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view7_octopusDualRun5_optimal2.gif" width="800" /> </br>
  The animations below show the octopuses on the two sides aligning to the central octopus. For illustrating the complexity of geometrical transitions involved in the shape alignments, both the front and top views are shown. <br>
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view7_octopusDualRun2_optimal.gif" width="800" /> </br>
  <i> Front View </i> <br>
  <img src="https://github.com/gasingh/shapeAlignment/blob/main/240601_icp_view7_octopusDualRun3_topView.gif" width="800" /> </br>
  <i> Top View </i> <br>

## Process of Development
Mesh: Decimated Neferetti with 4594 faces, 2502 vertices.  
  
Initially all the code was written in an external Python file (Python 3.4 in VSCode) . And then the interfacing with the 3d software was with custom data readers which were written inside Rhino3D to read matrix generated outputs from the mesh aLignment solver code, as meshes/ point clouds inside the 3d environment. So as you will see below, the code the optimization is run in the IDE on the right (VSCode), and the output is copy pasted to the clipboard. We are able to regenerate 3d point clouds and 3d meshes from computed point matrices, inside Rhino 3D by reading the clipboard memory.   

Later on, the tool was downgraded to Python 2.7 (the officially supported Python version for Rhino v7.0, 2024!). And the entire mesh alignment compute can happen directly inside it as a new Rhino command.

<img src="https://github.com/gasingh/shapeAlignment/blob/main/240530_icp_view5_nefertiti.gif" width="450" /> </br>

_GIF 2: Mesh Alignments integrated as a functionality inside Rhino3d._
