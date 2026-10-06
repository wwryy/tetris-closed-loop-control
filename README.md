# 🎮 Tetris Closed-Loop Control

A vision-based closed-loop control platform for **state perception, simulation, heuristic decision-making, neural policy learning, and automatic execution**.

This project was developed as the foundational verification stage of a broader reinforcement-learning platform for robotic systems.

Rather than treating Tetris simply as a game implementation, the project uses it as a compact environment for validating the complete engineering loop:

**Perception → State Representation → Decision → Action → Environment Feedback**

---

## 🔍 Overview

Before developing reinforcement-learning systems for high-dimensional robotic tasks, it is useful to verify the fundamental interaction pipeline in a smaller and more controllable environment.

Tetris provides:

- clearly defined environmental states
- discrete actions
- immediate feedback
- deterministic game mechanics
- repeatable simulation
- visual observations from a real interface

The project therefore uses Tetris to validate the main components required for later robotic closed-loop control.

---

## 🧠 System Pipeline

The complete workflow is:

```text
Real Tetris Interface
        ↓
Screen Capture
        ↓
Visual State Extraction
        ↓
Structured Board State
        ↓
Simulation Environment
        ↓
Heuristic Decision Policy
        ↓
State–Action Data Generation
        ↓
Neural Policy Learning
        ↓
Automatic Control
        ↓
Updated Visual Observation
```

This creates a complete perception–decision–execution–feedback loop.

---

## 👁️ Visual State Extraction

The first stage converts the real Tetris interface into a structured state representation that can be processed by control algorithms.

The perception pipeline includes:

- locating the game window
- screen capture
- manual region-of-interest selection
- image preprocessing
- color-space-based foreground extraction
- board-state reconstruction
- continuous state updates

The extracted state provides a bridge between the visual game interface and downstream policy modules.

---

## 🕹 Simulation Environment

A separate Tetris simulation environment was constructed using **Pygame**.

The simulator implements the core game mechanics required for repeatable policy development and debugging, including:

- piece generation
- horizontal movement
- rotation
- falling
- collision detection
- piece locking
- line clearing
- environment reset
- board-state export

Unlike the real interface, the simulator provides direct access to internal states, making it easier to test decision logic before transferring the controller back to the visual interface.

---

## 🧮 Heuristic Decision Policy

A rule-based search policy is used as the initial decision-making baseline.

For each falling piece, the controller evaluates feasible placements and compares the resulting board states using handcrafted structural features.

The heuristic considers factors such as:

- completed lines
- holes
- stack structure
- surface variation
- landing position
- well structure

The best candidate placement is selected as the reference action.

This heuristic is not intended to be the final controller. Its main role is to provide a stable baseline and generate reliable action references for later policy learning.

---

## 🗂 State–Action Data Generation

During heuristic execution, the system records:

- current board state
- current piece information
- current pose
- selected target pose
- selected target position

These observations and actions form a state–action dataset.

This stage verifies the same general idea required in later learning-based robotic systems:

```text
Environment State
        ↓
Reference Policy
        ↓
Action Selection
        ↓
Training Sample
```

---

## 🧠 Neural Policy Learning

A neural policy is trained to approximate the behavior of the heuristic controller.

The architecture combines two information sources:

### Board-State Branch

A convolutional network extracts spatial features from the reconstructed board state.

### Piece-State Branch

A fully connected branch processes information describing the current falling piece and its pose.

The two representations are fused before the network predicts the target action.

The resulting policy replaces explicit heuristic search during inference.

---

## 🔁 Closed-Loop Automatic Control

The trained policy is integrated back into the real Tetris interface.

The controller continuously performs:

```text
Screen Capture
      ↓
State Extraction
      ↓
Piece Recognition
      ↓
Policy Inference
      ↓
Target Action
      ↓
Keyboard Control
      ↓
Updated Screen
```

Additional execution logic is used to improve robustness during real-interface control, including:

- window locking
- command timing
- rotation mapping
- action correction
- frame-based state updates

This produces a complete closed-loop control system operating directly through visual observations.

---

## 🤖 Why Tetris?

The purpose of this project is not simply to develop a Tetris-playing program.

Instead, Tetris serves as a small-scale verification environment for engineering concepts that later appear in robotics:

| Tetris System | Robotics Analogy |
|---|---|
| Visual board recognition | Sensor-based state perception |
| Structured board state | Robot/environment state representation |
| Simulation environment | Robot simulation |
| Heuristic controller | Baseline / expert policy |
| State–action dataset | Demonstration or policy data |
| Neural policy | Learned control policy |
| Keyboard execution | Robot action interface |
| Updated screen | Closed-loop sensor feedback |

This staged approach makes it possible to debug the perception–decision–execution pipeline before moving to higher-dimensional humanoid and welding-robot systems.

---

## 🛠 Technologies

### Computer Vision

- OpenCV
- screen capture
- ROI extraction
- HSV-based image processing
- visual state reconstruction

### Simulation

- Pygame
- custom Tetris environment
- collision and game-state logic

### Policy & Learning

- heuristic search
- Dellacherie-style evaluation
- PyTorch
- convolutional neural networks
- supervised policy approximation

### Control

- real-time state updates
- keyboard-based automatic execution
- closed-loop visual feedback

### Programming

- Python

---

## 👩‍💻 Project Role

This project was completed as part of a team Keystone project on reinforcement-learning platforms for confined-space humanoid welding robots.

I served as the **group leader** and participated in the development, integration, testing, and organization of the staged verification platform.

The work formed the foundational algorithmic stage before the project progressed to humanoid motion learning and robotic welding simulation.

---

## 🔗 Connection to Robotics

The Tetris platform verifies several capabilities later reused conceptually in robotic systems:

- perception-to-state conversion
- repeatable simulation
- baseline policy construction
- training-data generation
- neural policy representation
- automatic action execution
- closed-loop feedback

The broader project subsequently extends these ideas to humanoid motion tracking and confined-space robotic welding.

---

## 📁 Repository Structure

```text
tetris-closed-loop-control/
│
├── assets/
│   └── images/
│
├── src/
│   ├── perception/
│   ├── simulator/
│   ├── policy/
│   └── control/
│
├── README.md
└── .gitignore
```

Selected project materials and demonstrations will be added progressively.

---

## 📄 Project

**Reinforcement Learning Platform for Confined-Space Humanoid Welding Robots**

Foundational Closed-Loop Verification Stage  
Keystone Project  
Fan Gongxiu Honors College  
Beijing University of Technology

---

## 🔗 Related Projects

- 🦾 **Humanoid Motion Learning** — video-driven motion recovery, retargeting, tracking-policy learning, and cross-simulation validation
- 🤖 **Task-Registered Robotic Welding Framework** — sim-to-real perception, RGB-D geometry recovery, weld-path generation, and robot interfaces

---

## 📬 Contact

**Weiran Wang**  
Beijing University of Technology  
Mechanical Engineering  
Second Bachelor's Degree in Computer Science and Technology
