# Writeup: Visualize the point-cloud 

## Range Image
![image](https://user-images.githubusercontent.com/84423466/164984829-a143d0cd-5b2e-4773-905f-7076f4e0fc21.png)
![image](https://user-images.githubusercontent.com/84423466/164984842-12de04f6-b759-4fdd-b39a-c64777af024b.png)


## BEV Map Visualization
From the point cloud visuals, some of the features are easily identifiable:
1) Tires
2) Rear-view mirrors
3) Front Windows
4) Far away vehicles

![MirrorsTires](https://user-images.githubusercontent.com/84423466/149856910-588df24d-25cc-4147-8129-b9fd12e30858.png)
![Front Window](https://user-images.githubusercontent.com/84423466/149856938-5e792cc3-52f1-4109-b252-c8e025966721.png)
![FarAwayVehicles](https://user-images.githubusercontent.com/84423466/149856960-88fc4973-3098-4e98-be12-c85441d72512.png)

## BEV from Lidar PCL
![image](https://user-images.githubusercontent.com/84423466/164984483-b72c093a-4cd6-4f04-bfa4-1ae3c5a3dde7.png)

## Intensity Layer
![image](https://user-images.githubusercontent.com/84423466/164984504-bbde0088-a01f-4bb5-bc46-6e8e5ee9b5a3.png)

## Height Layer
![image](https://user-images.githubusercontent.com/84423466/164984516-23378eff-b393-4a5f-9436-e5da00f66913.png)

## Density Layer
![image](https://user-images.githubusercontent.com/84423466/164984525-b3c72281-933a-4769-83dc-0184a1a3517c.png)

## Model-based Object Detection in BEV Image
![image](https://user-images.githubusercontent.com/84423466/164983057-93268c34-a7d7-4cb7-8608-fdc90d4d4b4b.png)
![image](https://user-images.githubusercontent.com/84423466/164983419-2f707f4f-457a-4a19-be9c-93c603e0e677.png)

## Performance Evaluation for Object Detection

![image](https://user-images.githubusercontent.com/84423466/164982516-b0085cbf-f09c-416f-9507-2cbe07dde4ba.png)
![image](https://user-images.githubusercontent.com/84423466/164982557-b572a209-83f7-499e-be1b-3f61089d06e7.png)
![image](https://user-images.githubusercontent.com/84423466/164982631-64f632ac-969e-43c6-b4ed-0149f2a8b0f1.png)


![image](https://user-images.githubusercontent.com/84423466/164934374-0e1744f9-9cb2-47d9-aa43-d9dac8b2134f.png)
![image](https://user-images.githubusercontent.com/84423466/164934311-b9515566-57af-488b-bcfd-e8fe1fa72fbd.png)

![image](https://user-images.githubusercontent.com/84423466/164934821-df72f0c3-9545-40fc-8247-499d0221ab24.png)
![image](https://user-images.githubusercontent.com/84423466/164934694-5ffffb54-1570-4195-a804-dacc96310e91.png)



# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?
In the first step, I implemented the Kalman Filter's basic code - Predict and Update. The system matrix, F and covariance matrix, Q, had to be made three dimensional. 
![Step 1 RMSE](https://user-images.githubusercontent.com/84423466/173482765-5fe53799-ae6d-4128-8338-df3c6c33b354.png)

In step 2, I did track initialization and track management activities, assuming Lidar sensor only. This was kind-of difficult to get right. I used the score as described in the classroom - # of detections in a window. My code had a bug, which I discovered when I reached step 3.
![Step 2 RMSE](https://user-images.githubusercontent.com/84423466/173482794-9c306410-9268-46d9-b809-53ed3c8d27c9.png)

In step 3, I implemented multi-object tracking, which was not very different from the classroom approach.
![Step 3 RMSE](https://user-images.githubusercontent.com/84423466/173482809-aa2e2cef-9dc7-462b-be0d-641aac197647.png)

Finally, in step 4, I filled in the code to calculate the non-linear measurement function get_hx(x). It took a lot of time to understand the rotation and translation concepts that were implemented in get_H(x).

### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 
If we are talking about efficiency, I'd say a lidar-only system will be sufficient 99% of the time. But since human lives are involved, 99% is not good enough. So the redundancy provided by a camera is critical. I did not see a difference in RMSE after introducing the camera in Step 4. 

### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?
One challenge I faced during the project was when camera measurements were not coming in, and it was reducing the score of a track, causing them not to get confirmed. If a sensor malfunctioned, and the sensor measurements stop coming in, legitimate tracks can get deleted.

### 4. Can you think of ways to improve your tracking results in the future?
A more adaptive track scoring and management module might be useful in improving tracking results.
