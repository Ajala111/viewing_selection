# viewing_selection
___

**Unmanned Aerial Vehicle (UAV) have gained lots of popularity over the past few years, as the technology has become more advanced and drones have becomes more cheaper (Besada, et. al., 2018). This has allowed the use of drones in many sectors such as photography, surveillance, filmmaking, as well as delivery systems. In this study, an approach was proposed to implement the adaptive view planning for aerial 3D reconstruction (with minimum number of images and optimized path) based on (Peng and Isler, 2018). This approach was mainly divided into two parts. Firstly, a method which will build the adaptive viewing planes or rectangles that can result in better viewing selection around the 3D object; and secondly, building of an optimized trajectory to cover the entire scene that ascertain the production of high-quality reconstruction.**

*Keywords: path planning, drone, optimized, adaptive viewing rectangle, clustering

### Pipeline:

![image](https://user-images.githubusercontent.com/56730691/201192277-99e19dff-0443-4668-be18-162cf6da694b.png)


The following steps must be executed in order to obtain optimized path using the Adaptive Viewing Rectangles approach;


### 1. Clustering of faces:

The 3D object was divided into series of triangles (triangular mesh), and location of faces are acquired using the centre-points of each triangular mesh. The height points of these centre locations are in 3D coordinates of the meshes.
Clustering of faces were performed based on their locations (using K-means clustering). However, there exists levels of difficulties when directly using a clustering algorithm on set of points due to possibly lack of prior information on the number of clusters that can adequately fits into the data. The elbow method similar to (Sampath and Shan, 2008) and (Molada-Tebar, et. Al., 2020) were adopted  

### 2. Construction of the Adaptive Viewing Rectangles (AVRs)

This is the crucial step for building rectangles to patch of clusters. Rectangular planes were fitted to each cluster earlier obtained and AVRs are constructed in such a way that they are parallel to the scene at specific viewing distance (d) which greatly depends on the user’s camera resolution and sensor. The viewing distance was integrated with the tolerance to favour the resolution of the views.

### 3. Viewing grids:

Viewing grids are imposed on the already created viewing rectangles, these grids are the collections of viewpoints on the rectangle with resolution. Points of grids are treated as the camera viewpoints. The orientation of this grid is set in normal direction to the fitted planes on clusters.

### 4. Optimized camera positions:
After imposing the viewing grids on the rectangles, iterate through all the center points (faces) of the mesh. For each face, sets of cameras that are contained within the visibility cone of the points were obtained. The same procedure was followed until all the faces are adequately covered. The implementation followed the view selection algorithm presented by (Peng and Isler, 2018), that is, the visibility cone must contain minimum of three camera views.

### 5. Trajectory Planning:

This is sub-divided into the following steps:

i.	Obtaining the Traveling Salesman (TSP) tours that traverse the optimized camera positions in each adaptive viewing rectangles

ii.	Forming the distance matrix and compute the minimum distance between two viewing grids using the edge that connect the viewing grids. Hence, minimum spanning tree were computed from distance matrix.

iii.	Computing the final tours (path) that visit all the optimized points in each rectangle following the tours earlier obtained.

___
 
*Besada, J.A., Bergesio, L., Campaña, I., Vaquero-Melchor, D., López-Araquistain, J., Bernardos, A.M., and Casar, J.R., 2018. Drone Mission Definition and Implementation for Automated Infrastructure Inspection Using Airborne Sensors*

*Molada-Tebar, A., Marqués-Mateu, Á., Lerma, J. L., and Westland, S., 2020. Dominant Color Extraction with K-Means for Camera Characterization in Cultural Heritage Documentation*

*Peng, C., Isler, V., 2018. Adaptive view planning for aerial 3d reconstruction. Available: https://conservancy.umn.edu/handle/11299/216033

*Peng, C., and Isler, V. 2018. View selection with geometric uncertainty modeling. Robotics: Science and Systems 2018, Pittsburgh, PA, USA

*Sampath, A., and Shan, J., 2008. Building roof segmentation and reconstruction from LiDAR point clouds using clustering techniques. The International Archives of the Photogrammetry, Remote Sensing and Spatial Information Sciences. Vol. XXXVII. Part B3a. Beijing
