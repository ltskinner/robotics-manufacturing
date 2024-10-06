# Chapter 5 - Path-Planning

- `path`
  - geometrical description of the robots movement in space
  - there are infinite paths between two
    - a straight line is the most simple, but any other curve can be programmed
  - different from `trajectory`
- `path planning`
  - deriving the equations of the curve that connects the starting and ending points of a movement
  - operator chooses curve, curve gets translated into mathematical equation which gets executed with a time-specific trajectory
- `point to point movement (PTP)`
  - planned in joint space
  - linear interpolation of the joint axes of the robot
  - offer no control over the actual path fo the end effector
    - simple to program and fast to execure
    - inherently unsafe bc cannot predict behavior in path space
  - **important:** a PTP movement is the only movement that allows a modification of the actual joint configuration
  - PTP movements are typically used for jogging individual joint axes, with the intention of moving one single link of the robot **without caring about the actual path of the TCP**
  - PTP movements are time-optimal (they always take the shortest possible time to complete)
  - these are typically "nice to have" but not as practical as path interpolated (which follow a specific, and expected path)
- `path-interpolated movement`
  - planned in path space
  - starting and ending points must be expressed in path-space coordinates
  - this is where quaternions come in
- `quaternions`
  - do not suffer from singularities
  - can be renormalized at any time whic makes them very robust against approximations
- `SLERP`
  - Spherical Linear intERPolation
- `transition`
  - the point of contact between two consecutive segments of a path
  - sharp edges are undesirable bc drop in speed
- `degree of continuity C^k`
  - C0 non-tangental transition
  - C1 tangent (like circle into a line)
    - translates into same movement speed on both sides of thhe translation
  - C2 like doing a circle
    - requires different axial accellerations to hold the same path speed

## Types of path interpolations

- Line
  - simplest
  - both position and orientation of TCP change during movement
- Circle
  - need 3 points:
    - starting
    - target (ending)
    - one other (which can also be the target point)
  - note, these cannot be colinear (all points lie in the smame line in space)
- Spline
  - Unreasonable to expect operators to know the math
  - So, have them give two points, and then we generate a spline
    - somewhere between a line and a circle lmao
  - Multiple points
    - P0 - starting point
    - PX - intermediate control point
      - these are usually not touched by the curve
      - defining
        - what direction
        - what magnitude
      - the curve moves away from the two edge points
      - typically just want two of these
      - rule of thumb: their distance from the corresponding edge point is about 1/3 of the linear distance between start and end point
    - PN - target ending point

## Path length
