# Chapter 3 - Forward Kinematics

- `forward transformations`
  - aka direct transformations
  - calculate position and orientation (opse) of TCP given the **current values of the joint axes**
- `inverse transformations`
  - calculate the values of the joint axes **given the current TCP pose**
- `home position`
  - when all joint axes have zero value
- `zero frame` == `base frame`
  - the additional offset and rotation between the global coordinate system (GCS) and the base of each robot
  - includes translational offsets as well as rotations across DoFs (like wall or ceiling mounted)
  - must express resulting TCP positions in the GCS
- `tool frame`
  - need this as well
- `mechanical coupling`
  - a coupling between two axes means the movement of one is internally (mechanically) linked to that of another axis
  - so, if motor fires it may move something in another axis which just is
- `coupling coefficient`
  - the difference function between coupled and non-coupled axes
