# Chapter 10 - Calibration

The firmware is developed as a generic piece of software and must always be parameterized and tuned to the specific robot it is controlling. This opperation is called calibration and is usually performed by the robots manufacturer before shipping the robot to the end user

Three sets of parameters to calibrate:

- the body of the robot
- the mounted tool
- the workspace cell

## Robot Calibration

Want to fine-tune:

- the mechanical sizes of links
- the angles between joints
- the encoder zero offsets

## Tool calibration

Once the robot body is calibrated, can be shipped to the customer for operation

Basically, if you drive the TCP to the same point from various positions, eventually a circle will be formed. The center of the circle is the real TCP. Procedure:

- Move the robot to reach the same TCP from several orientations
- Record the corresponding positions of the mounting point
- Build a system of equations from all the recorded positions
- Solve the system using the least-square estimation and find the TCP position
- calculate the tool size using the equivalence T = TCP - MP

## Cell Calibration
