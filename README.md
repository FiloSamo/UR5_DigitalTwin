# UR5 Robot Manipulator – Modeling & Simulation 🦾

*A simulation model of a UR5 robotic manipulator with PD + Gravity compensation control.*

---

## 📖 Overview
This project models and simulates the **UR5 robotic arm manipulator** using a modular approach based on:
- **Link and joint submodels**
- **Harmonic drive gear dynamics**
- **PD + Gravity compensation control**

The model has been developed using **Bond Graph** and custom submodels.

The goal is to validate the dynamic model and control strategy through simulation of a **pick-and-place trajectory** in joint space.

---

## 🛠 Features
- **6-DOF manipulator model** (UR5)  
- **Denavit–Hartenberg (DH) parameterization** for frame transformations  
- **Link dynamics** implemented via Euler equations  
- **Revolute joint constraints** for 1-DOF motion  
- **Harmonic drive submodel** with stiffness, damping, and gear reduction ratio  
- **PD + Gravity compensation controller** in the joint space
- **Trajectory planning** with cycloidal interpolation 

---

## 📐 Modeling Details

### Denavit–Hartenberg Convention

Frame transformations are implemented using **Modulated Transformers**, ensuring correct reference frames during simulation.

### Link Submodel

Each link is treated as a **rigid body with two-port connections**, exchanging forces and torques.
Dynamics are computed using Euler’s equations:

$$
\dot{p} = F - \omega \times p, \quad
\dot{h} = \tau - \omega \times h
$$

### Joint Submodel

Each revolute joint constrains motion to a single axis and computes joint angle θ as the integral of angular velocity.

### Harmonic Drive

Implements:

* Gear reduction ratio (e.g., HFUS-20: -1/100)
* Nonlinear stiffness with three constant regions $K_1, K_2, K_3$
* Viscous damping and static friction

---

## 🎛 Controller

The control law is:

$$
M(q)\ddot{q} + C(q,\dot{q})\dot{q} + D\dot{q} + G(q) = K_p e + K_d \dot{e} + G(q)
$$

where:

* $K_p, K_d$ are PD gains
* $G(q)$ is gravity torque compensation
* $e$ is the position error

---

## 📊 Simulation Results

* **Trajectory:** Three-point pick-and-place task
* **Trajectory profile:** Cycloidal in joint space
* **Results:**

  * Joint positions follow reference closely
  * Errors are small
  * Gravity compensation effective

---

## ✅ Conclusions

* The model accurately reproduces UR5 dynamics
* The PD + gravity compensation controller yields expected performance
* The framework is suitable for further **control design and testing**
* Future improvements: experimental validation with a real UR5 robot

---

## 📚 References

* A. Macchelli – *Modeling and Simulation of Mechatronic Systems M*, DEI – University of Bologna
* C. Melchiorri – *Industrial Robotics*, DEI – University of Bologna

---

## 👥 Contributors

This project was developed as part of the *Automation Engineering* course at the University of Bologna (AY 2024/2025).

| Name             | Role                     |
|-----------------|-----------------------|
| **Battistini Enrico** | Modeling & Simulation | 
| **Samorì Filippo**   | Controller Design & PD Tuning |
| **Subini Jacopo**    | Harmonic Drive Modeling & Report Editing |

💡 *Contributions were equally important in modeling, simulation, and documentation.*

---

## 📜 License

MIT License – See [LICENSE](LICENSE) for details.

```

