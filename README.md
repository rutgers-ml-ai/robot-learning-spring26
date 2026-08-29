# Rutgers IEEE ML/AI — Robot Learning Track (Spring 2026)

This repository is a meta-repo of teaching demos created for the **Robot Learning Track** of the Rutgers IEEE ML/AI Division during Spring 2026. The track introduced undergraduates to physics-based robot simulation with [MuJoCo](https://mujoco.org/) and the fundamentals of **imitation learning**, with supporting lectures on **reinforcement learning**.

## What This Track Covered

The track was designed as a hands-on progression from simulation basics to learning from demonstrations:

1. **MuJoCo fundamentals** — loading models, stepping a simulation, reading and writing joint states, and sending actuator commands in a visualizer loop.
2. **Imitation learning (behavior cloning)** — collecting expert trajectories with a motion planner, training a neural policy to mimic those demonstrations, and evaluating closed-loop performance in simulation.
3. **Reinforcement learning (conceptual intro)** — core ideas and how they relate to imitation learning, covered in the lecture slides below.

By the end, you should be able to walk through the full pipeline: simulate a robot, generate expert data, train a policy with supervised learning, and deploy it back in the simulator.

## Lecture Materials

| Topic | Slides |
| --- | --- |
| Imitation Learning | [Google Slides](https://docs.google.com/presentation/d/1mxmO_5_6dNUHYl2KWhCYNsFdRf-RWZUAMoJRIFscdls/edit?usp=drive_link) |
| Reinforcement Learning | [Google Slides](https://docs.google.com/presentation/d/1j5wcgHgYOXj9PZGtoKPwcTPl_woM7fivkYfWRFh078A/edit?usp=sharing) |

## Imitation Learning Workshop

The imitation-learning project was packaged as a standalone workshop. 

Follow the [repo README](https://github.com/kchen50/point-robot-imitation-learning/blob/main/README.md) for setup, implementation details, and the full workflow.

Pick whichever setup works best for you:

### Option 1: Google Colab (easiest — no local install)

If you don't want to set up MuJoCo and PyTorch on your machine, use the Colab notebook version. **NOTE: You need to save the notebook yourself and any additional files yourself, as the Colab instance will delete anytihng unsaved:

1. Open [`colab_friendly.ipynb` on Google Drive](https://drive.google.com/file/d/1qNIWkn854_rOreK9ZJCXgX4jMlD8swUK/view?usp=sharing).
2. Click **Open with → Google Colaboratory**.
3. Run the cells top to bottom. The notebook clones the repo, installs dependencies, and walks you through training and visualizing a behavior cloning policy.

Alternatively, you can open the notebook straight from GitHub in Colab — no Drive account needed:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kchen50/point-robot-imitation-learning/blob/main/colab_friendly.ipynb)

### Option 2: GitHub repo (local setup)

If you prefer running everything on your own machine:

```bash
git clone https://github.com/kchen50/point-robot-imitation-learning.git
cd point-robot-imitation-learning
pip install -r requirements.txt
```

## Repositories in This Meta-Repo

This repo bundles the demos as [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules). Clone everything at once with:

```bash
git clone --recurse-submodules https://github.com/rutgers-ml-ai/robot-learning-spring26.git
cd robot-learning-spring26
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

Each demo also lives in its own GitHub repo (linked below), so you can clone them individually if you only need one.

### [mujoco_demo](https://github.com/kchen50/mujoco_demo) — Intro to MuJoCo

Start here if you're new to MuJoCo. These are starter scripts for working with a Unitree A1 quadruped from the [MuJoCo Menagerie](https://github.com/google-deepmind/mujoco_menagerie):

| Script | What it demonstrates |
| --- | --- |
| `sim.py` | Load a scene, run the physics loop, and visualize in the passive viewer |
| `set_sim_state.py` | Directly set joint positions (`qpos`) and update the visualization |
| `set_action.py` | Send actuator commands (`ctrl`) and observe the robot respond |
| `mj_utils.py` | Helper functions for joint indices, state I/O, and collision checking |

These are the building blocks you'll need before moving on to learning-based control.

### [point-robot-imitation-learning](https://github.com/kchen50/point-robot-imitation-learning) — Behavior Cloning Workshop

This is the main hands-on project. You'll work through a complete imitation-learning pipeline built around a 2D point robot navigating obstacles in MuJoCo:

1. **Expert data collection** — an RRT motion planner generates demonstration trajectories (`collect_data.py`, `planner/`).
2. **Behavior cloning** — you'll implement supervised training in `train_behavior_cloning_policy.py` to learn a `Policy` from state–action pairs.
3. **Deployment** — run your trained policy closed-loop in simulation (`run_policy.py`).

Quick start (after cloning the repo):

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

See the [repo README](https://github.com/kchen50/point-robot-imitation-learning/blob/main/README.md) for full setup and implementation details.

## Suggested Learning Path

```
MuJoCo intro (mujoco_demo)
        ↓
Imitation learning lecture slides
        ↓
Workshop: RRT planner → data collection → behavior cloning → policy deployment
        ↓
Reinforcement learning lecture slides (contrast with imitation learning)
```

## Prerequisites

- Python 3.10+
- [MuJoCo](https://mujoco.readthedocs.io/en/stable/python.html) with the Python bindings (not needed if you use Colab)
- PyTorch (for the imitation-learning project)
- A machine with a display, or an X11/WSLg setup, for the MuJoCo passive viewer (local setup only)

## Acknowledgments

Developed as part of the Rutgers IEEE ML/AI Division Robot Learning Track, Spring 2026.
