# stereovision
Compute Stereo Vision on same objects taken from different viewpoints and obtain 3D informations

## 1. Introduction
The first image is a left rectified image of an industrial scene. The second image is a right rectified image of the same scene. 
The aim of this coursework is to compute the extraction of 3D information, given 2D images. It can be assimilated to the eyes process.
Each eye of the human body captures an independent image of the scene the body faces. As a result of the eyes computation, the person accesses to a 3D
environment.

## 2. Matching
The objective of this part is to find a way of obtaining matching points between the different images.

### 2.1. Candidate Matches
In order to associate points, the edges of the images are extracted. Indeed, it is well know that "all edge features along an epi-polar in the right image 
can form candidate matches with the edges from the left image".
In other words, given a row, each edge in the right image on this row is a candidate match of an edge in the left image on the same row.

In the code, the non-zero values one same rows are our candidate matches.
The dispary is computed for every couples of corresponding points. It is the difference of position between those pixels.

### 2.2. Cost Function
The cost function is used to judge about the consistency of the candidate matches.
Comparing pixel values together can be a solution with blinders. The context is that we used images from different viewpoints so values will probably by slightly different.
Instead of using this kind of technique, windows taken from candidate matches neighbors are adopted and compared to the left image considered as ground truth.
This comparison is made using Sum of Squared Differences (SSD in the code).

### 2.3. Best Match
After obtaining the cost of each candidate match, the task of selecting the best match has to be done. 
The candidate match, a point in the right image, that most look like a point in the left image will be picked. This similarity is expressed by the minimum match cost.

### 2.4. The Z Coordinates
The Z coordinate is defined as proportional to 1.0/(k+disparity), with k an arbitrary constant. Multiple values of k has been tested.

### 2.5. Real World Coordinates
For each group of matching points, the X coordinate is defined as : ((x_left * pixel_size * Z) / focal), with x_left the x left coordinate, Z the Z coordinate,
pixel_size the size of a pixel and focal the focal length of the camera used. 
The Y coordinate is defined as : ((y_left * pixel_size * Z) / focal), with x_left the x left coordinate, Z the Z coordinate, pixel_size the size of a pixel and focal the
focal length of the camera used.

## 3. Final Observation
The visualization can be done with Matplotlib in the Notebook environment in order to perform plot rotations as desired.
