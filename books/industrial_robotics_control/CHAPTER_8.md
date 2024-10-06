# Chapter 8 - Statics and Dynamics

- `hybrid control`
  - combining position and force control
- `wrench`
  - six-dimensinoal vector of forces and torques acting at a point in space

## Statics

Branch of physics that deals with forces

- important for contact-rich manipulation

## Singularities

## Dynamics

How much torque is required from each motor to generate a certain motion profile at the joints

## Dynamic Model

What parameters define the relationship of the link speed and acceleration with the applied motor torque:

- mass
- center of mass
- inertia
- motor inertia
- gear ratio
- friction
- stiffness

### Lagrangian Method

- conceptually more elegant, but computationally demanding, esp for robots with several degrees of freedom

### Newton-Euler Method

- can be effectively programmed for open chains of any number of axes
- basically, step thru link by link

### Parameter Identification

Use data-driven solution:

- more data is better
- high variety of data is better
- try to avoid generating response behavior that is not modeled by the equations
- focus on the behavior expected during actual application of the robot

## Torque Feed Forward

## Trajectory Optimization

Avoid situations that requires too much output torque from a motor

## Teach by Hand

- Have operator move the TCP to target pose and saving it. Do this a few times, and then the control software can automatically generate a trajectory that passes through them

## Motor Sizing
