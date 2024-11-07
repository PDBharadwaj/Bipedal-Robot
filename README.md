# Bipedal Robot
This repository provides an overview of the fundamentals, design, and hardware implementation of a bipedal robot. It focuses on the use of forward and inverse kinematics for leg movement control, maintaining stability through the center of mass balance concept, and integrating various hardware components to achieve a functional, walking bipedal robot.
## Key Features
- **Movement control**
- **Feasible design**
- **Stability**
- **Hardware integration**
## Concepts behind it and related tasks
### PID Control Theory
PID (Proportional-Integral-Derivative) control is a fundamental control theory that is used in control systems to maintain a desired output such as speed, position or temperature by continuously adjusting inputs based on feedback. A PID controller calculates the error as the difference between a desired setpoint (SP) and a measured process variable (PV). It then applies a correction based on three components: proportional, integral, and derivative terms.

- Proportional (P): The proportional term responds to the current error. It provides an output that is directly proportional to the error, allowing the system to correct deviations quickly.

- Integral (I): The integral term accounts for the accumulation of past errors. It helps to eliminate small errors that may not be fully corrected by the proportional term alone, achieving precise control over time.

- Derivative (D): The derivative part predicts future error by considering the rate of change of the error. It reduces overshoot and prevents oscillations by slowing down the system as it approaches the desired value.

### Task : Cruise Controller 
#### Aim
To develop a Cruise Controller using Python and Matlab(simulink) for maintaining desired set point velocity of a car.
#### Procedure
In Python
1. Set the mass of the vehicle(m) and the drag coefficient(b).
2. Define the set-point velocity(v=20 m/s).
3. Implement aPID controller in Python.
4. Determine the transfer function of the system.

In Simulink
1. Build the circuit of the cruise controller using the PID controller in Simulink.
2. Initially, set the integral gain (Ki) and derivative gain (Kd) to zero and tune the proportional gain (Kp).
3. After tuning Kp, tune the values of Ki and Kd to refine the controller's performance.
#### Result
The PID controller was successfully tuned to achieve:
- A rise time of approximately 10 seconds.
- A maximum overshoot of less than 5%.
