# Rutgers IEEE ML/AI — Robot Learning Track (Spring 2026)

This repository is a meta-repo of teaching demos created for the **Robot Learning Track** of the Rutgers IEEE ML/AI Division during Spring 2026. The track introduced undergraduates to physics-based robot simulation with [MuJoCo](https://mujoco.org/) and the fundamentals of **imitation learning**, with supporting lectures on **reinforcement learning**.

## What This Track Covered

The track was designed as a hands-on progression from simulation basics to learning from demonstrations:

1. **MuJoCo fundamentals** — loading models, stepping a simulation, reading and writing joint states, and sending actuator commands in a visualizer loop.
2. **Imitation learning (behavior cloning)** — collecting expert trajectories with a motion planner, training a neural policy to mimic those demonstrations, and evaluating closed-loop performance in simulation.
3. **Reinforcement learning (conceptual intro)** — core ideas and how they relate to imitation learning, covered in lecture slides (see below).

By the end, students could reason about the full pipeline: simulate a robot, generate expert data, train a policy with supervised learning, and deploy it back in the simulator.

## Lecture Materials

| Topic | Slides |
| --- | --- |
| Imitation Learning | [Google Slides](https://docs.google.com/presentation/d/1mxmO_5_6dNUHYl2KWhCYNsFdRf-RWZUAMoJRIFscdls/edit?usp=drive_link) |
| Reinforcement Learning | [Google Slides](https://docs.google.com/presentation/d/1j5wcgHgYOXj9PZGtoKPwcTPl_woM7fivkYfWRFh078A/edit?usp=sharing) |

The imitation-learning repo was also packaged into a standalone workshop:

- [Imitation Learning Workshop (PDF)](https://drive.google.com/file/d/1qNIWkn854_rOreK9ZJCXgX4jMlD8swUK/view?usp=sharing)

## Repositories in This Meta-Repo

This repo uses [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to bundle the demos. Clone with submodules to get everything:

```bash
git clone --recurse-submodules https://github.com/rutgers-ml-ai/robot-learning-spring26.git
cd robot-learning-spring26
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

### [`mujoco_demo/`](mujoco_demo/)

**Intro to MuJoCo simulation.**

Starter scripts for working with a Unitree A1 quadruped from the [MuJoCo Menagerie](https://github.com/google-deepmind/mujoco_menagerie):

| Script | What it demonstrates |
| --- | --- |
| `sim.py` | Load a scene, run the physics loop, and visualize in the passive viewer |
| `set_sim_state.py` | Directly set joint positions (`qpos`) and update the visualization |
| `set_action.py` | Send actuator commands (`ctrl`) and observe the robot respond |
| `mj_utils.py` | Helper functions for joint indices, state I/O, and collision checking |

These demos are the starting point for understanding how MuJoCo models, data (`MjData`), and actuators fit together before moving on to learning-based control.

- Submodule: [kchen50/mujoco_demo](https://github.com/kchen50/mujoco_demo)

### [`point-robot-imitation-learning/`](point-robot-imitation-learning/)

**Hands-on behavior cloning workshop.**

A complete imitation-learning pipeline built around a 2D point robot navigating obstacles in MuJoCo:

1. **Expert data collection** — an RRT motion planner generates demonstration trajectories (`collect_data.py`, `planner/`).
2. **Behavior cloning** — students implement supervised training in `train_behavior_cloning_policy.py` to learn a `Policy` from state–action pairs.
3. **Deployment** — run the trained policy closed-loop in simulation (`run_policy.py`).

Quick start (from inside the submodule):

```bash
cd point-robot-imitation-learning
pip install -r requirements.txt

# Visualize the RRT planner
python -m planner.rrt_core

# Train a behavior cloning policy (after implementing train_BC_policy)
python train_behavior_cloning_policy.py

# Run the trained policy
python run_policy.py
```

See the submodule's [README](point-robot-imitation-learning/README.md) for full setup and implementation details.

- Submodule: [kchen50/point-robot-imitation-learning](https://github.com/kchen50/point-robot-imitation-learning)

## Suggested Learning Path

```
MuJoCo intro (mujoco_demo)
        ↓
Imitation learning lecture slides
        ↓
RRT planner visualization → data collection → behavior cloning → policy deployment
        ↓
Reinforcement learning lecture slides (contrast with imitation learning)
```

## Prerequisites

- Python 3.10+
- [MuJoCo](https://mujoco.readthedocs.io/en/stable/python.html) with the Python bindings
- PyTorch (for the imitation-learning submodule)
- A machine with a display, or an X11/WSLg setup, for the MuJoCo passive viewer

## Acknowledgments

This was developed as part of the Rutgers IEEE ML/AI Division Robot Learning Track, Spring 2026.
