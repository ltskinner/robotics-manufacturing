# Chapter 2 - Geometric Framework

## Reference Frames

- `frame`
  - coordinate system with a specific position and orientation
  - when describing a position of a generic point in space, always need to do that relative to a specific frame
  - a point has different coordinates according to what frame we are using as reference
- `global coordinate system`
  - defines origina and orientation of the world
- `local coordinate system`
  - other machines will not see this
  - if one robot, global and local are the same
- `tool coordinate system`
  - origin located at thhe TCP of the robot
- `workpiece coordinate system`
  - what the robot operator sees
  - all programmed points and movements refer to this system
  - typically several of these in a working cell bc robot performs multiple tasks on many products

## Frame Operations

To convert between two points:

- translate and then rotate
- can also rotate and translate at the same time
- kinda think of this as updating the observation point, for the same absolute point

Frame Translation:

- `offset`
  - Delta = [dx, dy, dz]
  - these are linear operations

Frame Rotations

More complicated than translations bc not linear

- right hand rule
  - align thumb with axis, heel at origin

Properties of a Rotation Matrix

Composing Rotations: Euler Angles

- rotate around X-Y-Z
  - Roll, Pitch, Yaw
  - remember the order matters
- also the quaternions

The column vectors of a rotation matrix represent the axes of the old frame (before the rotation) as seen from the new frame (after the rotation)

Inverted Transformation

- if you can transform points from one frame to another, you can quickly learn to do the inverse
