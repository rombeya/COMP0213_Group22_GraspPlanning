# Grasp Planning Pipeline

**COMP0213 - Object Oriented Programming for Robotics and AI**

A grasp planning framework using PyBullet simulation and machine learning classification to predict grasp success for robotic manipulation tasks.

---

## What This Project Does

This project implements a complete grasp planning pipeline that:

1. **Generates grasp candidates** using sphere-based sampling around target objects
2. **Executes grasps in simulation** using PyBullet physics engine
3. **Collects training data** with labeled success/failure outcomes
4. **Trains ML classifiers** (Random Forest, SVM) to predict grasp success
5. **Tests the planner** on new, unseen grasp configurations

### Key Features

- **Object-Oriented Design**: Abstract base classes for Grippers and Objects with concrete implementations
- **Multiple Grippers**: PR2 Gripper and Panda-style Gripper
- **Multiple Objects**: Cube and Cylinder with different geometries
- **Balanced Dataset**: Includes both easy (likely success) and difficult (likely failure) poses
- **Classifier Comparison**: Evaluates Random Forest and SVM to select best performer

## Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager

### Install Dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install pybullet numpy pandas scikit-learn
```

---

## How to Run

Open the jupyter notebook file (projectOOP.ipynb). Run the first cell, then the second cell. 
The first cell contains all the definitions whilst the second cell runs the full pipleine.
The output should show all grasps, training and testing phase results, and the final results.

Also, download the urdfs and keep within the same directory

## Configuration

### Gripper-Object Combinations

| Gripper | Object | Object Position | Sampler Radius |
|---------|--------|-----------------|----------------|
| PR2 | Cube | [0.6, 0.3, 0.025] | 0.08m |
| PR2 | Cylinder | [0.6, 0.3, 0.05] | 0.06m |
| Panda | Cube | [0.6, 0.3, 0.025] | 0.08m |
| Panda | Cylinder | [0.6, 0.3, 0.05] | 0.06m |

### Dataset Features

| Feature | Description | Unit |
|---------|-------------|------|
| x, y, z | Gripper position | meters |
| roll, pitch, yaw | Gripper orientation | radians |
| success | Grasp outcome | 0 or 1 |

---

## Expected Results

- **Dataset**: ~140 samples with ~60% success, ~40% failure
- **Classifier Accuracy**: 80-90% on validation set
- **Test Accuracy**: 80-90% on new grasp configurations

---

## Class Diagram

```
GraspableObject (Abstract)          Gripper (Abstract)
       │                                   │
   ┌───┴───┐                         ┌─────┴─────┐
   │       │                         │           │
 Cube  Cylinder                  PR2Gripper  PandaGripper


GraspSampler ──▶ GraspSimulator ──▶ DataFrame ──▶ Classifier
```

---

## OOP Principles Used

1. **Abstraction**: Abstract base classes define interfaces
2. **Inheritance**: Concrete classes extend abstract bases
3. **Polymorphism**: Simulator works with any Gripper/Object type
4. **Encapsulation**: Internal PyBullet details hidden in classes


## References

- [PyBullet Documentation](https://pybullet.org/)
- [scikit-learn Documentation](https://scikit-learn.org/)
