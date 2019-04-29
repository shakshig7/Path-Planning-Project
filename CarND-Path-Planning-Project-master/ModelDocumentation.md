# Path Planning Project

## Goals
* To plan a path for the car to drive in a simulator with traffic
* To drive the car atleast upto 4.32 miles without collisions
* To change lanes when there is traffic ahead of you
* Maintaining Speed limit
* Avoid exceeding max accelaration and jerk

##  Path generating model
The model for generating paths can be broadly classified into 3 parts :

### Prediction
In the prediction part **(Refer to code 254 - 300)**,we are using the sensor fusion data and locating the lanes of other vehicles.
Once the lane is known,we will check the lane of other vehicle with our car fr speed & lane change and update the boolean variable.
* If there is a car in front of us blocking our way ,'car_in_front' is boolean true. 
* If there is a vehicle within the range of 30m in left lane,'car_in_left' is boolean true.
* If there is a vehicle within the range of 30m in right lane,'car_in_right' is boolean true.

### Behaviour
In the behaviour part **(Refer to code 302 - 339)**,we are updating the behaviour of the vehicle based on the position of other vehicles on road.
There are three possible behaviours for car to do when it is getting blocked by other vehicle
* If there is a left lane and 'car_in_left' is false i.e we can safely change to left lane.
* If there is a right lane and 'car_in_right' is false i.e we can safely change to right lane.
* If the two behaviours are not possible ,then we should remain in the current lane and reduce the speed gradually to avoid collision.

If our vehicle is not blocked by any other vehicle,then we just need to maintain our speed around the speed limit and avoid crossing max accelaration and jerk.

### Trajectory

In the trajectory part **(Refer to code 341 - 445)** , we calcualte the trajectory using the coordinates of our car,previous trajectory points and the behaviour.
* Spline is used for calculating the coordinates,and to make spline calculation easier ,coordinates are transformed to local car coordinates.
* The points used for spline calculation are previous trajectory points and if there is no previous trajectory,three points at adistance of 30m from each other are used in addition to car coordinaties for initialzing calculation.
* The speed of the car is updated on every trajectory point based on the speed difference which is measured at behaviour part.
