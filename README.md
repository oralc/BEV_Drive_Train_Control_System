# BEV Driveline Control System

## Description
This repository contains the Simulink model and MATLAB code developed for the BEV Driveline Control System project. The project focuses on modeling the driveline of a Battery Electric Vehicle (BEV), implementing a control system, and evaluating its performance using the Worldwide Harmonized Light Vehicles Test Procedure (WLTP) cycle.

## Table of Contents
1. [Methodology](#methodology)
    - [Driveline Modeling](#driveline-modeling)
    - [Resistance Modeling](#resistance-modeling)
    - [Control System Design](#control-system-design)
    - [WLTP Cycle Tracking](#wltp-cycle-tracking)
2. [Calculations & Model with Explanations](#calculations--model-with-explanations)
    - [3DOF Driveline Model & Driving Resistance Calculations](#3dof-driveline-model--driving-resistance-calculations)
    - [Motor Torque and Speed (1D Lookup)](#motor-torque-and-speed-1d-lookup)
    - [Motor Torque Limiting (Saturation Dynamics)](#motor-torque-limiting-saturation-dynamics)
    - [PID Control](#pid-control)
3. [Results and Interpretation](#results-and-interpretation)
    - [Discussion about the Max Speed of the Vehicle on Flat](#discussion-about-the-max-speed-of-the-vehicle-on-flat)
    - [Conclusion](#conclusion)

## Methodology
### Driveline Modeling
A Simulink model was constructed to represent the crucial components of the BEV's driveline. This includes the electric motor, transmission, side shafts, and a simplified representation of the vehicle, referred to as the 'reduced vehicle model'. Provided parameters such as stiffness, damping, and inertia were used to describe the physical characteristics of these components.

### Resistance Modeling
The total driving resistance (T_load) experienced by the vehicle was computed and modeled. This includes rolling resistance, air resistance, and acceleration resistance, considering factors such as vehicle speed, vehicle mass, drag coefficient, reference area, air density, and rolling resistance coefficient.

### Control System Design
A PID control system was implemented, using the speed error (the difference between the desired and actual vehicle speed) as its input to generate a torque command for the electric motor.

### WLTP Cycle Tracking
The desired vehicle speed from the WLTP cycle was imported and converted into a desired motor speed, used as the reference signal for the PID controller. The control system was tuned to ensure the actual vehicle speed closely follows this reference signal.

## Calculations & Model with Explanations
### 3DOF Driveline Model & Driving Resistance Calculations
- A 3DOF driveline model was developed to encapsulate the interactions of the electric motor, transmission, and a simplified vehicle model.
- Total driving resistance acting on the vehicle was calculated based on various driving resistance parameters.

### Motor Torque and Speed (1D Lookup)
- A 1D lookup table stores data about the relationship between motor speed (ω) and torque (T_mot). Given a certain motor speed, the lookup table provides the corresponding torque.

### Motor Torque Limiting (Saturation Dynamics)
- The Saturation block is used to limit the torque output of the motor, representing the physical limitations where increasing the input current beyond a certain point does not result in an increase in torque.
- Braking Torque Limiting: Ensures that the braking torque does not exceed a safe limit.

### PID Control
- The PID controller was used to control the motor torque to drive the vehicle at desired speeds as per the WLTP cycle.
- The proportional part of the controller responds to present speed errors, the integral part corrects for accumulated past errors, and the derivative part anticipates and mitigates potential future errors.

## Results and Interpretation
### Discussion about the Max Speed of the Vehicle on Flat
The maximum speed of the vehicle on a flat road is determined by the driveline model parameters, including the electric motor's maximum rotational speed, gear ratio, and dynamic wheel radius. The calculated maximum speed is 105 kph, limited by the constraints of the electric motor and driveline setup.

### Conclusion
Results from the 3DOF driveline model and the designed PID controller showed effective tracking of the WLTP cycle. The model accurately represents the BEV's dynamic behavior, and the controller efficiently managed the motor torque based on speed error.

## Files
- `BEV_Model_DTCS_Project_Oral.slx`: Simulink model file.
- `Variables.m`: MATLAB script for parameter definitions.
- `WLTP.xlsx`: WLTP cycle data.
