# ICP-3D
**ICP Algorithm for Rhino3D**

_The ICP algorithm can be used to match point clouds in a variety of applications, including robotics, computer vision, and 3D scanning. It is a powerful method for aligning point clouds and can be used to create high-quality 3D models from multiple scans or to register 3D objects in real time._


## Aim
- This is a native Python implementation for an ICP algorithm for Rhino3D.
- The aim is to be able to utilize this functionality inside the Rhino 3D environment.


## Pseudocode 

### Matching Point Clouds using ICP Algorithm

The Iterative Closest Point (ICP) algorithm is a widely used method for aligning two point clouds. The algorithm works by iteratively finding the best transformation that aligns the two point clouds.

Steps for matching two point clouds using the ICP algorithm:

1. **Initialize the transformation**: The ICP algorithm starts by initializing the transformation between the two point clouds.
2. **Find closest points**: For each point in the first point cloud, find the closest point in the second point cloud.
3. **Compute transformation**: Once the closest points have been identified, the ICP algorithm computes the transformation that minimizes the distance between the corresponding points in the two point clouds.
4. **Update transformation**: The computed transformation is then used to update the transformation between the two point clouds.
5. **Repeat**: Steps 2-4 are repeated until the transformation between the two point clouds no longer changes significantly.
