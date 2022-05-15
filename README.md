# Problem Summary: Vehicle Pose Transform by GAN for Re-Id KeyPoint generator
This is a discuss and record for the summary about "Vehicle Pose Transform by GAN for Re-Id KeyPoint generator" problem.
Now is working on the Sol.2., create another model to satisfy the GAN framework.

## Vehicle Pose Transform by GAN for Re-Id
The structure of system framework is below:
<center>
  
![圖片1](https://user-images.githubusercontent.com/55344725/168473344-81b4c2a1-d26e-4cd2-b66f-86cc5e644345.jpg)</center>

### With training
1. will input image `Input Image x` and a sequence with vehicle key-point `Target pose`.
2. `Generator` generate fake image with target pose in specific key-point, target pose is come from real image.
3. Compute Loss between fake image and real image, real image includes the target pose.

### With testing
1. will input image `Input Image x` without vehicle key-point `Target pose`.
2. `Generator` generate fake image in target pose with specific key-point.

## Problem Summary
### Problem
**In training**, not all vehicle have all type of pose, so `Generator` will lack some specific key-point.
we can not generate doesn't exist pose vehicle. The structure of training framework will become:
<center>
  
![圖片](https://user-images.githubusercontent.com/55344725/168477015-d927f987-18b8-46e9-9745-e224e57bbe87.jpg)</center>
without key-point, `generator` will fail to generate fake image.

### Solution
1. Take the average of the KeyPoints for each pose of all types, and use the average instead if a vehicle of a certain type does not have KeyPoint on a specific pose.
2. **Create another model for generate vehicle KeyPoint.**
3. If vehicle doesn't have KeyPoint on a specific pose, then use CycleGAN-like algo. to generate fake image, Else using original GAN.
