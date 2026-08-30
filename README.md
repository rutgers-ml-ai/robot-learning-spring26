# Rutgers IEEE ML/AI — Robot Learning Track (Spring 2026)

This repository is a meta-repo of teaching demos created for the **Robot Learning Track** of the Rutgers IEEE ML/AI Division during Spring 2026. By the end, you should be able to walk through the full pipeline: simulate a robot, train a policy to copy expert data using supervised learning, and deploy it back in the simulator.

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

## Lecture Materials

| Topic | Slides |
| --- | --- |
| Imitation Learning | [Google Slides](https://docs.google.com/presentation/d/1mxmO_5_6dNUHYl2KWhCYNsFdRf-RWZUAMoJRIFscdls/edit?usp=drive_link) |
| Reinforcement Learning | [Google Slides](https://docs.google.com/presentation/d/1j5wcgHgYOXj9PZGtoKPwcTPl_woM7fivkYfWRFh078A/edit?usp=sharing) |

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

### [mujoco_demo](https://github.com/kchen50/mujoco_demo) — Intro to MuJoCo

These are starter scripts for working with a Unitree A1 quadruped from the [MuJoCo Menagerie](https://github.com/google-deepmind/mujoco_menagerie):

| Script | What it demonstrates |
| --- | --- |
| `sim.py` | Load a scene, run the physics loop, and visualize in the passive viewer |
| `set_sim_state.py` | Directly set joint positions (`qpos`) and update the visualization |
| `set_action.py` | Send actuator commands (`ctrl`) and observe the robot respond |
| `mj_utils.py` | Helper functions for joint indices, state I/O, and collision checking |

### Imitation Learning Workshop

Instructions are included in [repo README](https://github.com/kchen50/point-robot-imitation-learning/blob/main/README.md). 

#### Option 1: Google Colab (no local install)

If you don't want to set up MuJoCo and PyTorch on your machine, use the Colab notebook version. **NOTE**: You need to save the notebook yourself and any additional files yourself, as the Colab instance will delete anything unsaved. It will also be slightly more difficult to navigate the relevant files in Colab.

1. Open [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qNIWkn854_rOreK9ZJCXgX4jMlD8swUK).
<!-- 2. Click **Open with → Google Colaboratory**. -->
2. Make a copy of the notebook. Click **File → Save a copy in Drive**.
3. Run the cells top to bottom. The notebook clones the repo, installs dependencies, and walks you through training and visualizing a behavior cloning policy.
4. If you are having trouble with implementing the policy yourself, you can still view the demos at [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kchen50/point-robot-imitation-learning/blob/main/colab_friendly.ipynb).

#### Option 2: GitHub repo (local setup)

If you prefer running everything on your own machine:

```bash
git clone https://github.com/kchen50/point-robot-imitation-learning.git
cd point-robot-imitation-learning
pip install -r requirements.txt
```
