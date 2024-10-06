# Chapter 6 - Workspace Monitoring

While we can produce paths, not always physically possible for the robots TCP to move along those curves

- `safe zone`
  - virtual cage for the robot
- `forbidden zone`
  - precludes the robot from entering certain areas of space
  - can be combined with safe zones as logical elements to describe complex space geometries
  - (e.g. forbidden zone within safe zone)
- linearization
  - `cuboids`
    - spaces can be linearized by representing areas as 3D shapes with 6 rectangular faces
    - these can be defined as just two points in space
    - also note - splines are expensive to compute. for the purpose of reprogramming, what if we just did c0 movements and purely linear? sure, harder on hardware, but if reprogramming time is more valuable then fuck it frfr
- self-collision
  - `capsules` - two spheres in a tube, pretty easy to compute
- `exlusive zones`
  - regions of space that only one robot (or at least its TCP) can occupy at any given time
- collision detection
  - collsion test: two capsules intersect if the distance between the capsules generating segments is smaller than the sum of their radii

## Collision monitoring and detection

- the sooner we can predict a collision, the better
  - wise to monitor the path while planning it, not just while executing it
  - cases where monitoring in advance isnt possible:
    - position of other robots in the same workspace is commanded by other controllers and the info about their path is not available to our control software
    - when dealing with external additive corrections commanded by sensors or cameras. these are added at real time, after the path has been planned, and as such require dynamic monitoring

## Linearization

- both points of a path may be inside a safe area, but the actual path could intersect a forbidden region of space

## Wire-frame mModel

## Safe Orientation

## Self-Collision

relies on `capsules` - two spheres in a tube, pretty easy to compute
