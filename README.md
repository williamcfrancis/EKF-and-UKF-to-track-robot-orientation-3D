# Extended Kalman Filter and Unscented Kalman Filter for 3D Robot Orientation Tracking
## Overview
Kalman filtering, also known as linear quadratic estimation (LQE), is an algorithm that uses a series of measurements observed over time, including statistical noise and other inaccuracies, and produces estimates of unknown variables that tend to be more accurate than those based on a single measurement alone, by estimating a joint probability distribution over the variables for each timeframe. It works good, but the downside of using Kalman Filter is that it only works for linear systems.

The next generation of KF was the Extended Kalman Filter (EKF) and it was a successful filter because it takes account to non-linearity. The only drawback with EKF is that it’s too difficult to do in real time practice at a microcontroller. Note that EKF is just a linearized KF by using jacobians, which is not very easy to use in practice. Therefore, another filter was created to replace EKF, it was Unscented Kalman Filter (UKF) and it was the most successful kalman filter ever made. 

Here I developed the UKF for the IMU data and the vicon data for calibration and tuning of the filter, this is typical of real applications where the robot uses an IMU but the filter running on the robot will be calibrating before test-time in the lab using an expensive and accurate sensor like a Vicon.

As reference for the UKF implementation, I used this paper - [A quaternion-based unscented Kalman filter for orientation tracking](https://ieeexplore.ieee.org/document/1257247) by Edgar Kraft

## Data
The data consist of observations from an inertial measurement unit (IMU) that consists of gyroscopes and accelerometers and corresponding data from a motion-capture system called Vicon. See [this video](https://www.youtube.com/watch?v=qgS1pwsHQIA&ab_channel=TravisErickson) to get a better understand of the Vicon system.

The data is provided as .mat files in /imu and /vicon folders.

## Run
To run the EKF algorithm, run extended_kalman_filter.py\
To run the UKF algorithm, uncomment the last line in the Unscented_kalman_filter.py file to call the function estimate_rot

## Results
### Extended Kalman Filter
Plotting the true value of a and the estimated value of a along with their low and high variance estimates.
![image](https://user-images.githubusercontent.com/38180831/205469328-7f96646c-09b6-40bc-a1e3-936ca763afd1.png)

### Unscented Kalman Filter
#### Plotting the mean of quaternion q and the quaternion corresponding to the vicon orientation:
![image](https://user-images.githubusercontent.com/38180831/205468844-3e5bcec9-5ab4-450d-9e02-c0e64e0b384c.png)

#### Plotting the covariance of quaternion q:
![image](https://user-images.githubusercontent.com/38180831/205468857-061caf34-6b4e-4eb3-aa7e-9e659a318c45.png)

#### Plotting the mean of angular velocity:
![image](https://user-images.githubusercontent.com/38180831/205468869-ba60d938-56b4-4591-a3c2-4e96a7259dc7.png)

#### Plotting the diagonal of covariance of angular velocity:
![image](https://user-images.githubusercontent.com/38180831/205468883-2b306e83-1517-4d7a-989c-e83cd905b441.png)
