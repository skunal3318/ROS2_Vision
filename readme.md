<p align="center">
  <img src="https://raw.githubusercontent.com/ros-infrastructure/artwork/master/ros_logo.svg" alt="ROS 2 Logo" width="450">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/ROS2-Jazzy-blue" alt="ROS2 Jazzy">
  <img src="https://img.shields.io/badge/Simulation-Gazebo-green" alt="Gazebo">
  <img src="https://img.shields.io/badge/Vision-OpenCV-orange" alt="Vision">
  <img src="https://img.shields.io/badge/Status-Active-success" alt="Project Status">
</p>

**Vision-Based Lane Following Rover** is a **simulation-first autonomous mobile robot** developed using **ROS 2 (Jazzy)** and **Gazebo (gz-sim)**.  
The project focuses on **camera-based perception and closed-loop control**, where the rover follows a visual lane using classical computer vision techniques (OpenCV).

---

## 🌟 Why This Project?

This project was built to:
- Learn **vision-driven autonomy** in ROS 2
- Understand **camera → perception → control** pipelines
- Implement **closed-loop steering control** without heavy planners
- Build a strong foundation before adding mode switching or hardware

Unlike LiDAR-based navigation, this project emphasizes **visual perception as the primary decision source**.

---

## 🚗 Rover Capabilities

- 👁 **Camera-Based Lane Detection**
- 🛣 **Autonomous Lane Following**
- 📐 **Centroid & Error-Based Steering Control**
- 🎥 **Gazebo Camera Sensor Integration**
- 🔌 **ROS2 Topic-Based Control (`cmd_vel`)**
- 🧪 **Fully Simulated in Gazebo (gz-sim)**

---

## 🧠 System Architecture

The rover follows a clean and modular ROS 2 design:

- **Gazebo Simulation**
  - Rover model (URDF/Xacro)
  - Camera sensor
  - Custom lane world
- **ROS2 Nodes**
  - Image acquisition (`/camera/image_raw`)
  - Vision processing (OpenCV)
  - Control logic (velocity commands)
- **Visualization & Debugging**
  - RViz2
  - `rqt_image_view`
  - Debug image overlays

This modular separation allows easy extension to **real hardware** later.

---

## 👁 Vision Pipeline (Core Logic)

The lane-following behavior follows this pipeline:

1. **Camera Image Capture**
2. **Region of Interest (ROI) Extraction**
3. **Color Thresholding (HSV)**
4. **Morphological Filtering**
5. **Lane Centroid Detection**
6. **Lateral Error Computation**
7. **Proportional Steering Control**

This approach avoids black-box ML models and keeps the system **interpretable and tunable**.

---

## 🧭 Control Strategy

- **Linear Velocity**: Constant forward speed  
- **Angular Velocity**: Proportional to lateral lane error  

```text
angular_z = -Kp × (lane_center − image_center)
```


## ▶️ How to Run

```
# Build the workspace
colcon build
source install/setup.bash

# Launch the rover in Gazebo
ros2 launch rover_bringup rover.launch.xml

# Run the vision-based lane following node
ros2 run rover_vision lane_follower.py

