# Chapter 9 - Firmware

The core control system of the robot. Where the kinematics and dynamics calcs occur and where the operators commands are transformed into actual robotic movement. Writing firmware is the most challenging task for a robotics developer

Core firmware functions:

- `HMI`
  - reads comands and parameters from the operator. This is the interface beteween the outside human world and the internal machine world
- `interpreter`
  - translates the input commands into motion instructions
- `main controller`
  - plans a path and generates a trajectory
  - in practice, translates motion instructions into target position and torque values
- `servo drives`
  - drives the motors to move the robot
  - controls the behavior of the electric motors according to the values set by the main controller
- `online programming`
  - programming a robot through the HMI, using teaching or testing functions
- `offline programming`
  - more commonly, programs are automatically generated, tested, and tuned using simulation
  - after developed, uploaded to robot
- `robot programming`
  - input a sequence of actions that the robot will then execute in automatic mode
  - done through the HMI
  - actions can be described as:
    - lines of text
    - graphical icons
- `open-loop`
  - a control system that operates without feedback
  - washing machine runs for fixed ammount of time, regardless of moisture measures
- `closed-loop`
  - feedback is used to change control signals

## HMI

Three main functions:

- Configuration
  - where users can modify the values of the robots parameters:
    - mechanical dimensions
    - joint and path limits
    - zero position offsets
    - workspace zones dimensinos
    - dynamic profiles
    - motors and encoder settings
    - servo loop gains
- Movement programming
  - usually split between:
    - manual control
    - automatic control
- Diagnostics
  - Like telemetry crap
    - position of all joints and TCP axes in different coordinate systems
    - temperature and current of all motors
    - eventual warnings or errors triggered during operation
    - log files

HMI doesnt need to run on real-time OS

- handheld panel with an Arm processor and a Windows IoT OS
- decentralized generic device, consumer tablet running android(more commonly)
- Xamarin is good for HMI, uses .NET so spans android, windows, and iOS

## Interpreter

The HMI provides an interface for the user to program the robot

Actions are described either as text or graphically. Interpreter needs to parse and translate these into low-level motion instructions for the motion libraries to use

ML P1 Z1 T1 = "move linear to P1 defined in frame Z1 using tool T1"

ML P3 FA100 = moving at 100 mm/s

- FC = feed rate cartesian speed
- FA = Feed rate Angular speed
  - The speed setting carries on until the next one is set

MC P2 Q1 F10 = move circle, needs to have Q1 additional point along the path

Example:

- ML P1 R100 FC100
- ML P2 R50
- ML P3 R100
- MC P5 Q4 R100
- MC P7 Q6

Length of circle can be forced with an angel H, which can either be positive or negative and range across several revolutions like H-720. This also has priority over target P, and the end of the movement may not correspond to P

MS P1 F100 = Move Spline to point P1 at Force 100/s

MJ = Move joint

HOMe F100 = move all joint axes to their zero position

## Motion Commands

| Command | Description | Parameters |
| - | - | - |
| ML | Linear interpolation of the path axes | **P**, F, Z, T, R |
| MJ | Linear interpolation of the joint axes | **P**, F, Z, T, R Ji |
| MC | Circular interpolation of the path axes | **P**, **Q**, F, Z, T, H |
| MS | Spline interpolation of the path axes | **P**, F, Z, T |
| HOME | Move joints to their home (zero) position | F |

## Parameters for Motion Commands

| Parameter | Description | Notes |
| - | - | - |
| P | Target position | |
| F/FC/FA | Path angular speed Generic/Cartesian/Angular | Units depend onf speed defintion |
| Z | Frame index | 0 is base frame |
| T | Tool index | 0 is no tool |
| Q | A point on the circle path | Must not be collinear with P |
| H | Rotation angle | |
| R | Round edge radius | Must be a nonnegative value |
| Ji= | Optional reference value for joint axes | Only used for MJ with target point specified in path axes |

There are some others, like TRK for track to (de) activate a conveyor-tracking synchronization

- MJ P0 F100
- TRK 1 // synchronize with Conveyor # 1
- ML P1 F100
- ML P2 F100
- TRK 0 // desynch from Conveyor # 1
- ML P3 F100

Another is TANG for (de)activation of a tangental axis. typically used with an asymmetric tool for cutting or grinding operations, a tang command forces the orientation of the TCP to be always aligned with the path, when projected over a surface (usually, the X-Y plane). TANG 1 activates, TANG 0 deactivates

## Auxiliary Commands and Statements

| Command | Description | Parameters |
| - | - | - |
| TRK | Start tracking conveyor | [0, index] |
| TANG | (De)activate tangental tool | [0,1], H |
| T | Modify active tool (without movement) | [index] |
| WAIT | Delay time | [seconds] |
| WAIT DI | Wait for a digital input signal to be TRUE | [index] |
| SET DO | Set a digital output signal | [index] |
| RESET DO | Reset a digital output signal | [index] |
| M | M-function to communicate with main controller | [index] |
| IF..ELSE | Conditional statement | |
| GOTO | Jump to a specified label | Label, Loop count |
| SUB | Execute local subroutine at specified label | Label, Loop count |
| LABEL: | Any string followed by ":" | |
| END | Abord main program execution or return from subroutine | |
| // | Comment | |

## Main Controller

The main controller is the brain of the robot: it reads input commands (from the HMI, the IOs, the actuators encoders), performs all the necessary motion calculations, and generates output instructions for the servo drives

The most important software components of the main control program are:

- interpreter
- path planner
- set point generator
- and the motions buffer

All motion instructions are inserted into a `motion buffer`, and the interpreter keeps an index counter so that it always knows where to insert the new parsed information (buffer is circular with infinite length)

## Kernel Interface

Three key parts of common structure:

- Commands
  - The actions called by the application software to control the robot
- Parameters
  - The configuration of the robot and commands
- Monitor
  - A detailed view of the current status of the robot

## Robotics Libary

### Commands Structure

| Command | Description |
| - | - |
| Run program [auto mode] | Starts the execution of a user program, from the selected line number until the end line or end of file |
| Jog axis [manual mode] | Jogs an axis along a specific direction, either in the path space or in the joint space |
| Stop | Stops the current movement (both in automatic and manual mode) |
| Halt | Halts the current movement (only in automatic mode) |
| Continue | Continues a halted movement |
| Reference | Sets the position of the joints and auxiliary axes to the actual values read from the encoders |
| Reset | Resets all active errors |
| Calibrate | Runs the calculations for tool or frame calibrations |
| Identify | Runs the calculations for dynamic model identification |

### Parameter Structure

| Parameter | Description |
| - | - |
| Mechanics | Type of kinematic model (e.g. SCARA, Delta, six-axes manipulator, etc), links size, joints coupling, zero frame |
| Jiont axes limits | Limit values for the position, speed, acceleration, and jerk of each joint axis |
| Auxiliary axes limits | Limit values for the position speed, acceleration, and jerk of each auxiliary axis |
| Path space limits | Limit values for the path speed (linear and angular), acceleration, and jerk |
| Motor units | Conversion factor between the joint units and the actual motor units: includes gear ratio, encoder scaling, and direction |
| Workspace | Configuration of all the safe and forbidden zones, the orientation cone, the links capsules radii for self-collision and inter-collision detection |
| Calibration | An interface to the tool and frame calibration functions: accepts input values for recorded measurements and returns estimated frames positions and orientations |
| Dynamics | An interface to the dynamic model parameters and their identification function |
| Actual joint positions | Read directly from the encoders and used when referencing the axes at start-up |
| User program | Provides the interface to the user program that must be parsed by the interpreter. It can be input either as a text file or intabular format |
| Start\stop lines | The starting and ending lines for automatic program execution. By default, the whole program is normally executed |
| Single step mode | Specifies whether the program execution should be continuous or step-by-step |
| Simulation | Specifies whether the calculated axes positions should be sent to the servo drives or not |
| Override | A percentage speed reduction for testing purposes |
| Points | A list of target points taught by the operator an used during program execution. Each point specifies the target position of the robot axes, either in the joint space or in the path space. Auxiliary axes values can also be provided. POints given in the path space are valid in their corresponding workpiece frame |
| Frames | List of local workpiece framse taught using the frame calibration procedure and used during program execution |
| Tools | List of tools to be mounted on the robot and used during program execution. Their size represents the geometrical distance between the MP and TCP and can be identified using the tool calibration procedure |
| Jogging configuration | An interface for the manual movement command: axis to be jogged (joint axis, path axis in base frame or tool frame, auxiliary axis), direction, speed, optional target position |
| Conveyor | Frame configurations of the conveyors to be tracked and real-time position to be followed by the robot |
| Path corrections | External offset corrections provided by the applciation program and applied to the patha xes. These values are not included in path-planning phase, and care should be taken to avoid uncontrolled axes movements |
| Filter time | Specifies the filter time for the output position values sent to the servo drives. Larger values smooth out the movement dynamics but also cause larger deviations from the planned path |

### Monitor Structure

| Variable | Description |
| - | - |
| Robot status | Current status of the robot (e.g. standstill, moving, halted, error, etc.) |
| Path status | Current TCP speed and position [X, Y, Z, A, B, C] |
| Joint axes status | Current speed and position of the joint axes |
| Auxiliary axes status | Current speed and position of the auxiliary axes |
| Set positions | Calculated motor positions to be setn to the servo drives. They already include compensations for the gear ratios, encoder scaling and direction, homing offsets |
| Set torques | Calculated motor torque values to be sent to the servo drives |
| Line number | Shows the line number of the user program currently being executed in automatic mode |
| Block length | Shows the total length and already completed length of the currently executed movement |
| Target point | Shows the coordinates of the target point for the currently executed movement |
| Tool/frame | Shows the currently active tool/frame |
| Error | Shows the number and detailed information of any active serror. Also, shows the line number that triggered the error in the user program |

## Servo drives

Typically recieve set values fro mthe main controller and then uses **closed-loop** contro lsystem (servo loop) to calulate the voltage applied at each stage

Usually a cascaded PID

**feed-forward** **open-loop* control

Closed loop means there is feedback. Open means its just gonna run

## Electronic Commutation
