# 3D_Object_Tracking

I fused the camera and lidar data to track objects in 3D space, and implemented TTC  algorithms for a collision detection system.
1. load image (into ring buffer from KITTI dataset), load lidar 3D point cloud data, load camera and lidar calibration data (rotation matrix and translation)
2. using YOLO to detect and classify objects in image, generate 2D objects BoundingBox in image
3. crop lidar points, remove lidar points out of ROI
4. cluster lidar points whose projection into the image falls into the same bounding box, loop over all Lidar points and associate them to a 2D bounding box.
5. detect keypoints from current image(Harris, SIFT, BRISK) and extract keypoints descriptors(SIFT, BRISK) (opencv build-in functions)
6. matching keypoints between current image and previous image
7. associate bounding boxes between current and previous image using keypoint matches to realize tracking of 3D object boundingBox, (data association) )
8. calculate TTC with lidar data of each object (take the median x-distance as the chosen distance to avoid work with outlier)  
9. group keypoint matches into a given BoundingBox in image
10. calculate TTC with camera, Compute time-to-collision (TTC) based on keypoint correspondences in successive images
