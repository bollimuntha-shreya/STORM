# STORM: Fast Joint-Space Model-Predictive Control for Reactive Manipulation

---

## Overview
STORM (Stochastic Trajectory Optimization for Robot Motion) is a sampling-based Model-Predictive Control (MPC) framework for reactive robot manipulation in dynamic and unstructured environments. Unlike task-space MPC frameworks, STORM performs **joint-space optimization**, enabling explicit handling of kinematic constraints, joint limits, and self-collision avoidance.  

This project adapts the original STORM framework (designed for Franka Emika Panda) to the **xArm7 manipulator**, validating its performance for real-time reactive manipulation tasks, including dynamic obstacle avoidance and trajectory tracking.

---

## Features
- **Joint-Space MPC:** Optimizes control sequences directly in joint space for kinematic feasibility.
- **GPU-Accelerated Rollouts:** Parallelized trajectory sampling using PyTorch for real-time performance up to 125 Hz.
- **Reactive Planning:** Handles dynamic and static obstacles with perception-driven or geometric cost functions.
- **Adaptation to xArm7:** Updated kinematics, collision models, and control loops for compatibility with a 7-DOF xArm7 robotic manipulator.
- **Real-Time Execution:** Runs control loop at 100 Hz with low-level torque commands at 1000 Hz.

---

## System Setup
- **Hardware:** xArm7 7-DOF manipulator, NVIDIA GPU-enabled workstation
- **Software:** Python, PyTorch, ROS (for xArm7 communication)
- **Collision Model:** Approximate collision spheres for xArm7 links
- **Control Loop:** Joint acceleration-based, with filtered state estimation

---

## Methodology
1. **Rollout Sampling:** Sample N joint acceleration sequences over a horizon H. Predict future states using forward kinematics in parallel.
2. **Cost Function:** Weighted sum of:
   - Pose Cost (end-effector target)
   - Smoothness Cost (joint accelerations)
   - Joint Limit Cost
   - Manipulability Cost (avoid singularities)
   - Optional Collision Cost (geometric or learned)
3. **Distribution Update:** Update Gaussian distribution over controls using softmax-weighted average (MPPI).
4. **Execution:** Execute first control in mean trajectory; warm-start next iteration.

---

## Results
- Real-time reactive motion planning and obstacle avoidance on xArm7.
- Smooth, feasible joint trajectories while respecting kinematic constraints.
- Demonstrated successful transfer of STORM from Panda to xArm7.

---

## References
- [STORM Original Paper by Nvidia]([https://github.com/your-link-here](https://research.nvidia.com/publication/2021-11_storm-integrated-framework-fast-joint-space-model-predictive-control-reactive))  


## Code
- [GitHub Repository](https://github.com/yourusername/STORM-xArm7)
