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

---
### Task 1: Cruise Controller 
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

[Cruise controller](https://hackmd.io/_uploads/SyKU5ti5C.png)

### Mechanics and Control of Robotic Manipulators

Watched the YouTube playlist on Mechanics and Control of Robotic Manipulators: <br>
https://www.youtube.com/playlist?list=PLyqSpQzTE6M-tWPjnJjFo9sHGWxgCnGrh

---

### Task 2: Finding FK/IK of Arm Manipulator in XY Plane in Python Using matplotlib 
#### FORWARD KINEMATICS (FK)
1. **Construct the DH Table**:
    - Defined the Denavit-Hartenberg (DH) parameters for the manipulator.
    - Used these parameters to create the DH transformation matrix.
2. **Implement the DH Transformation Matrix**:
    - Inputted the DH transformation matrix in Python.
3. **Develop the Forward Kinematics Function**:
    - Created a function that sequentially multiplies transformation matrices to compute the end-effector position.
    - Post-multiplied the matrices according to the manipulator's configuration.
4. **Define FK Parameters**:
    - Set up the necessary parameters for forward kinematics.
    - Inputted the specific values corresponding to the desired assembly configuration.
  
[Result graph1](https://hackmd.io/_uploads/r1ypsFi9C.png)
[Result graph2](https://hackmd.io/_uploads/Hy8k2KjcC.png)
#### Result
- Successfully defined the DH parameters and transformation matrices.
- The forward kinematics function accurately calculates the end-effector position for the specified assembly.

#### INVERSE KINEMATICS (IK)
1. **Construct the DH Table**:
    - Defined the Denavit-Hartenberg (DH) parameters for the manipulator.
    - Used these parameters to create the DH transformation matrix.
2. **Implement the DH Transformation Matrix**:
    - Inputted the DH transformation matrix in Python.
3. **Develop the Inverse Kinematics Function**:
    - Create a function to calculate the relative inverse kinematics (IK) parameters for the desired assembly configuration.

[Code image](https://hackmd.io/_uploads/S1h-VqicA.png)
#### Result
- Successfully defined the DH parameters and transformation matrices.
- The inverse kinematics function accurately calculates the necessary joint angles for the specified end-effector position.

---

### Task 3: Simulating an Arm Manipulator in XYZ Plane in Python Using matplotlib 
#### PROCEDURE
**Choose a Method for Simulation:**:
- We can use one of the following approaches:
-   **Denavit-Hartenberg (DH) Method**
-   **Closed-Form Solution**
-   Numerical Analysis
-   Geometrical Method

1. Using the DH Method:
   - Defined the DH parameters and construct the DH transformation matrix.
   - Written the inverse kinematics (IK) function to determine the joint angles for the intended trajectory.
2. Using the Closed-Form Solution:
   - Defined the forward kinematics (FK) equations for the required trajectory, at first.
   - Then, solved these FK equations to obtain the IK parameters.
   - Later, ploted the simulation based on these parameters.
- Our task was to trace the trajectory of a sine wave and a line by 3DoF Arm manipulator using inverse kinematics. We went with the geometrical method to find the equations of the joint angles.

[Result image3](https://hackmd.io/_uploads/By8LkHSWJx.gif)
[Result image4](https://hackmd.io/_uploads/BJlDkrSWkg.gif)

#### Result
- Successfully simulated the arm manipulator in the XYZ plane using the chosen method.
- The IK parameters were accurately determined, and the manipulator followed the intended trajectory in the simulation.

---

### IMPLEMENTATION ON PROJECT
- We decided to make 2dof manipulator as Bipedal Robot legs.
- Formed the inverse kinematics equations and solve them on the Sinusoidal trajectory followed by retracment of Straight Line trajectory backwards.
- Here is the python pseudocode for finding ik solutions:
```python
def inverse_kinematics(x, y):
    r = sqrt(x**2 + y**2)

    if r > (a1 + a2):
        raise ValueError("Target is not reachable")

    cos_theta2 = (r**2 - a1**2 - a2**2) / (2 * a1 * a2)
    cos_theta2 = np.clip(cos_theta2, -1.0, 1.0)
    sin_theta2 = sqrt(1 - cos_theta2**2)
    theta2 = atan2(sin_theta2, cos_theta2)

    theta1 = atan2(y, x) - atan2(a2 * sin(theta2), a1 + a2 * cos(theta2))

```


[Result image5](https://hackmd.io/_uploads/rJNpf4H-yx.gif)

#### Result
- Successfully simulated the 2DoF in XY Plane according to the required trajectory.

---


### DESIGNING THE ROBOT
- We used Autodesk Fusion 360 Software to create the CAD model for our 2DoF robot.
- After creating the model for one leg, we mirrored it for the other leg.
- Here is the final model that we came up with.
[Cad model](https://hackmd.io/_uploads/HkIrL97-yx.gif)

---

### HARDWARE IMPLEMENTATION
We used 3 main components in our project.
1. 6 servos, with 3 in each leg. One in hip, one in knee and one in foot(to balance the COM while the robot is walking).
2. Arduino UNO to connect all electronic equipments.
3. PCA9685 with a 5V power supply to connect and power multiple servo motors easily.
From the previous python code for sine and line we stored the calculated joint angles at each instance into a text file and uploaded those angles into the arduino code. Hence the servos will rotate at the desired angle which will help the biped to trace the require trajectory and walk forward.

---

### FINAL IMPLEMENTATION
Final implementation video:  <br>
https://drive.google.com/file/d/1ExQmth9Wmd_ic7VYFRZv-HQTB80MoZfJ/view?usp=sharing
