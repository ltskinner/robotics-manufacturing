# Chapter 7 - Trajectory Generator

- `trajectory`
  - a function that samples points from the path s along the time t
- `jerk`
  - derivative of acceleration over time
- `time-optimal movement`
  - a trajectory that traverses a path as fast as possible, still without violatingg the given dynamic constraints
- `twist`
  - spatial velocity = twist = jacobian x joint velocities

## S-Curve Profile

Generating a tranjectory with constant speed form start to end is mathematically valid, but not physically realistic

7 distinct regions:

- initial increase of acceleratio with limited jerk
- a phase of limited acceleration
- a decrease of acceleration with limited jerk to reach maximum speed
- a central area of constant limited speed
- three more zones similar to the initial three, reducing speed to 0 with limited acceleration and jerk

## Sinusoidal Profile

## Bezier Profile

## Time-Optimal Movements

The speed profiles theory works well for individual axes (for jogging to a single point) and their direct interpolations (i.e. PTP movement). We can easily set the speed, acceleration, and jerk limitations for an axis based on its motor and mechanics

However, the same principle does not immediately apply to path interpolated movement. The relation between a path and joint space is highly nonlinear, especially near singular points: setting a maximum speed value for the interpolated path trajectory does not impose any speed limitations on the individual axes

## Differential Kinematics

## Path Speed Definitions

In a practical software implementation, we let the operator decide what kind of speed definition to use for each programmed movement. We then calculate the length of the movement in that particular coordinate system (cartesian or quaternion). Once the movement length is known, we can apply the trajectory generating algorithm to the specific block

## Optimal Motion in Practice

Thus far, considered trajectory limitations forced by constraints on the joints speed

However, we normally also want to impose constraints on higher orders of derivative: limiting acceleration and jerk makes the movement visibly smoother, gentler on the mechanics, and also more conservative on the motors currents

Optimizing a trajectory can be simplified enomeously if the underlying path is well optimized in the first place. rounding edges, ptp movements instead of path planning is good, rerouting to stay clear of singularities. can also cheat and filter out the generated trajectory in the time domain

## Time filtering

- gaussian filter

## External Path Corrections

Why bother adding time filters in the joint space if we already have the ability to properly optimize the trajectory in the path space?

- trajectory optimization is a complex task to implement
- not all movements by the robot are processed by the trajectory generator
