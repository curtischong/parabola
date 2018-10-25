# SE 101 Project Proposal

## Goal: To track a ball moving in midair with cameras and predict where it will land. The landing location will be highlighted with an augmented reality overlay

## Hardware Involved
 - 3 60fps / 1080p cameras with a USB output
 - A modern laptop

## Evolutionary Prototype
 -  We want to approach the task with an evolutionary prototype because we know that as we implement different components (discussed further below) such as object tracking, augmented reality overlays, etc, we will need to tweak parts of the codebase since the project requirements are still not well-defined. We plan on having a verticle prototype because proper implimentation of object tracking is essential for other parts of the project to be developed. Without this component, an MVP is not feasable.

## Features:
 - Object triangulation in the X-Y-Z volume with three cameras.
     - 30fps object detection
 - Augmented reality overlay that highlights the landing location and path trajectory

## Integration:
Our project will include a 10m x 10m x 10m cubic volume viewed by three 30fps 1080p cameras. Two cameras will be placed perpendicular to each other, on adjacent edges of the volume, and the third will be placed above the volume. These cameras will feed the raw image data into a single laptop that will identify the location of the ball in each of the three images, locate the ball in the 3d space using the calculated locations, notify an external augmented reality device where the ball will land on the plane.

## Ball Identification
The ball will be painted bright neon green (or pink) to distinguish itself from background colours. We will develop a convolution matrix that will return a high value if it detects a round, neon object. We will run a series of convolution matrices on received frames to identify the ball’s location. After the ball is first detected, we will optimize detection expanding the search area, starting at the known original location of the ball. Once the ball has been detected in two subsequent frames, we can use the kinematics equations to predict the ball’s likely area in following frames, further decreasing our search space and optimizing our search time. 

## Augmented Reality
The augmented reality device will receive streaming data from the detection server about the ball’s location. It will use this data to display a trail through the air, showing the ball’s past and future path, as well as an overlay over the ball itself, with arrows representing it’s current velocity vector.  

## Path Prediction
 - Kinematic Equations

## Possible Concerns
 - Object Detection Speed: 
     - Object detection must be run on three high-resolution frames simultaneously. Therefore, the detection must be implemented with efficient algorithms, in a fast language (C/C++/Rust), running on fast hardware.
 - Camera Synchronization
     - Cameras must capture frames as close to simultaneously as possible, or timestamps must be retrieved from cameras, to ensure that position calculations do not conflict between perspectives. 
 - Network Latency
     - To allow for 30fps image processing, total system latency must be kept below 30ms. Thus, data must be transferred over the local network to minimize network latency. 
 - Localization of the AR Camera:
     - The augmented reality viewing device must know it’s position relative to the coordinate system used in object detection to accurately display information about the ball.

## Milestones
Oct 25: Finish ball detection
Oct 30: Determine the position of the ball in 3d space
Nov 7: Integrate the calculations with AR Kit.
Nov 15:  Finish project
Nov 21: Finish bug bashing/optimizations

