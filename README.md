# ICP-3D
**ICP Algorithm for Rhino3D**

![](https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240531_043415%20-%20Copy.jpg)

_The ICP algorithm can be used to match point clouds in a variety of applications, including robotics, computer vision, and 3D scanning. It is a powerful method for aligning point clouds and can be used to create high-quality 3D models from multiple scans or to register 3D objects in real time._

_This is an implementation of the ICP inside Rhino. All the math is coded independently inside pure Python with no external code. The ICP is embedded inside Rhinocommon API, to leverage direct access to Rhino 3D point clouds and meshes._

`#machine-learning` `#statistics` `#linear-algebra` `#applied-maths` `#3d` `#geometry`

## Aim
- This is a native Python implementation for an ICP algorithm for Rhino3D.
- The aim is to be able to utilize this functionality inside the Rhino 3D environment.

## Use Cases
- Accurate comparison of 3d Meshes.
- Automated alignment of shape parts in 3d space.
- AEC Industry: (Facade Components and manufacturable assemblies) Very useful to estimate similarity of facade geometries, and shape verification.


## Demonstration of ICP inside Rhino 3D on various datasets
  
### 1. Stanford Bunny
  Mesh: Decimated Stanford Bunny with 178 faces, 95 vertices.
  
  <img src="https://github.com/gasingh/ICP-3D/blob/main/240530_icp_view1.gif" width="800" /> </br>
  <img src="https://github.com/gasingh/ICP-3D/blob/main/240530_icp_view2.gif" width="800" /> </br>
  
### 2. Octopus
  Mesh: High Resolution Octopus with 3436 faces, 1752 vertices.
  <img src="https://github.com/gasingh/ICP-3D/blob/main/240530_icp_view3.gif" width="800" /> </br>
  <img src="https://github.com/gasingh/ICP-3D/blob/main/240530_icp_view4.gif" width="800" /> </br>

## Process of Development
Mesh: Decimated Neferetti with 4594 faces, 2502 vertices.  
  
Initially all the code was written in an external Python file (Python 3.4 in VSCode) . And then the interfacing with the 3d software was with custom data readers which were written inside Rhino3D to read matrix generated outputs from the ICP solver code, as meshes/ point clouds inside the 3d environment.  

  <img src="https://github.com/gasingh/ICP-3D/blob/main/240529_ICP-DemoPts_real-time-rec_example2_presentationVersion3_final_reduced2_240601.gif" width="800" /> </br>

_GIF 1: ICP calculated externally and the final results read by Rhino 3d._

Later on, the tool was downgraded to Python 2.7 (the officially suppoted Python version for Rhino v7.0, 2024!). And the entire ICP compute can happen directly inside it as a new Rhino command.

<img src="https://github.com/gasingh/ICP-3D/blob/main/240530_icp_view5_nefertiti.gif" width="450" /> </br>

_GIF 2: ICP integrated as a functionality inside Rhino3d._

___

<details>
<summary> <h4> Pseudocode </h4> </summary>

## Pseudocode 

Matching Point Clouds using ICP Algorithm

The Iterative Closest Point (ICP) algorithm is a widely used method for aligning two point clouds. The algorithm works by iteratively finding the best transformation that aligns the two point clouds.

Steps for matching two point clouds using the ICP algorithm:

1. **Initialize the transformation**: The ICP algorithm starts by initializing the transformation between the two point clouds.
2. **Find closest points**: For each point in the first point cloud, find the closest point in the second point cloud. (CORRESPONDENCES)
3. **Compute transformation**: Once the closest points have been identified, the ICP algorithm computes the transformation that minimizes the distance between the corresponding points in the two point clouds.(COMPUTE SVD, TO GET (R,t) FOR APPROPRIATE ROTATION & TRANSLATION OF THE DATASET).
4. **Update transformation**: The computed transformation is then used to update the transformation between the two point clouds. (REALIGN POINTS)
5. **Repeat**: Steps 2-4 are repeated until the transformation between the two point clouds no longer changes significantly. (CHECK FOR CONVERGENCE, EITHER BY AN ITERATION LIMIT/ A CONVERGENCE TOLERANCE LIMIT)
6. **Additional Considerations**: It is noted that the ICP sometimes never converges, as it gets stick by finding a local minima. We addressed this problem by implementing rotation clones of the input mesh via PCA, along the identified principal axes. We iteratively iterate this multiple rotation dataset over the above implemented ICP solver to find successful convergence. (CONVERGENCE MEASURES)



</details>

<details>
  <summary><h4> Exercises </h4></summary>

<p align="center" width="100%">
<b> EXERCISES </b> <br> <br>
<b> Exercise 1: Transformations based on homogenous matrices </b> <br> <br>
  <img src="https://github.com/gasingh/ICP-3D/blob/main/240429_translate%26rotateUsingPyrePython_00.gif" width="800" /> </br>
<b>GIF 1</b> </br> A proof of concept to illustrate the (R,t) implementation when R and t are extracted from SVD!
</p>

___

<p align="center" width="100%">
<b> Exercise 2: PCA based one shot alignments </b><br>
  Exercise 2 is an alignment tool with one shot alignments of similar shape meshes in Rhino 3d! So select a parent and select a child, the child aligns itself to the parent in one shot! <br>
<img src="https://github.com/gasingh/ICP-3D/blob/main/240508_pca_kettle-3d-mesh-alignment_try3_preview.gif" width="500" /> </br>
<b>GIF 1</b> </br> A proof of concept to align meshes in one shot by PCA!<br>
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240509_020634.jpg" width="250" /> 
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240509_021815.jpg" width="250" /> </br>
<b>Image Set 1</b> </br> Alignment of tea-pot geometries based on a parent geometry reference!
</p>

___

<p align="center" width="100%">
<b> Exercise 3: PCA based one shot alignments: SymmetryCorrections </b><br>
Exercise 3 is an alignment correction procedure applied to the initial alignment tool. We perform a post-alignment mesh intersection check, if there is an error alignment, we recompute the PCAs and flip the PCA axes, and realign, until there is a perfect match. <br>
<img src="https://github.com/gasingh/ICP-3D/blob/main/240509_pca_bunnies_alignmentErrors_symmetry.gif" width="400" />
<img src="https://github.com/gasingh/ICP-3D/blob/main/240509_pca_bunnies_alignmentErrors_symmetry_FIX.gif" width="400" /> <br>
<b>GIF 1,2</b> </br> PCA alignment symmetry error!(LEFT), and the FIX (right)<br>
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_024959.jpg" width="300" />
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_024402.jpg" width="300" />
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_031145.jpg" width="300" /> <br>
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_031012.jpg" width="300" />
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_031436.jpg" width="300" />
<img src="https://github.com/gasingh/ICP-3D/blob/main/ViewCapture20240510_025004.jpg" width="300" /> </br>
<b>Image Set 2</b> </br> PCA doesnot know the orientation direction of the agglomeration always, so vectors can get flipped!
<img src="https://github.com/gasingh/ICP-3D/blob/main/240509_pca_bunnies_alignmentErrors_symmetry_FIX-DEMO.gif" width="500" /> </br>
<b>GIF 3</b> </br> We try and fix the orientation problem, by recomputing PCAs and flipping the axis vectors, until overlap converged is met. But this too is not 100% solid in finding the correct alignments. This limitation is addressed by the ICP algorithm which works with point correspondences, by 1:1 mappings/ by nearest neighbour searches. <br>
</p>

</details>

