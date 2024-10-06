# Chapter 4 - Inverse Kinematics

Why do we need an inverse kinematic funciton if we already know the value of the joint axes from the motors encoders?

- this is a good point but we also want to have the ability to predict where the joints need to be driven to, given a desired target pose for the robots TCP
- this information is essential for planning future movements and executing them

## Definitions

- `path space`
  - robots typically programmes by operator like [X, Y, Z, A, B, C]
- `joint space`
  - [J_1, ...., J_6]
- `singularity`
  - two or more robots joints align in a way they become redundant, so lose a DoF and its no longer clear which joint should rotate
  - when large number of number of IK solution

Issues with Inverse Kinematics:

- Nonlinear Problem:
  - kinematics model is highly nonlinear
    - moving TCP along straight line does not mean joint axes are moving linearly
  - nonlinearities are extreme around singularities
- Nonunique Solution:
  - the generic pose of the TCP may be reached by more than one configuration of the joint axes
    - the solution of an inverse transformation is not alwaus unique
  - factors to consider when selecting solution:
    - Safety
    - Distance (less is better usually)
    - Forced (by operator preference what they like, or for reasons not easy to encode)
