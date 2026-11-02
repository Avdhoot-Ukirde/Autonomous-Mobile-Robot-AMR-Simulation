# Autonomous Mobile Robot (AMR) Simulation

**A differential-drive robot simulated in Gazebo that builds a map of its environment with SLAM and then navigates it autonomously using ROS 2 Nav2.**

ROS 2 project, Robotics and Artificial Intelligence, MGM University (Jawaharlal Nehru Engineering College, JNEC).

<!-- TODO: add a demo GIF or video link here. This matters most for a simulation project.
![AMR demo](docs/demo.gif)
[Watch the full demo video](PASTE_VIDEO_LINK) -->

---

## What it does

1. **Models** a differential-drive robot with a LiDAR sensor, described in URDF/Xacro.
2. **Simulates** the robot and its sensors in Gazebo.
3. **Maps** indoor environments by running SLAM Toolbox on the LiDAR data to produce a 2D occupancy grid.
4. **Navigates** autonomously with Nav2, planning a global path to a goal and avoiding obstacles with a local planner and costmaps.

## Tech stack

| Area | Technology |
|------|------------|
| Middleware | ROS 2 |
| Simulation | Gazebo |
| Robot description | URDF / Xacro |
| Sensor | 2D LiDAR |
| Mapping | SLAM Toolbox |
| Navigation | Nav2 (global and local planning, costmaps) |
| Visualization | RViz2 |

<!-- TODO: write the exact versions you used, e.g.
ROS 2: <distribution>, Gazebo: <version>, Ubuntu: <version> -->

## Requirements

- Ubuntu with ROS 2 installed
- Gazebo and its ROS 2 bridge packages
- Nav2 and SLAM Toolbox

```bash
sudo apt install ros-<distro>-navigation2 ros-<distro>-nav2-bringup ros-<distro>-slam-toolbox
```

Replace `<distro>` with your ROS 2 distribution name.

## Getting started

```bash
# 1. Create a workspace and clone the repo
mkdir -p ~/amr_ws/src && cd ~/amr_ws/src
git clone https://github.com/Avdhoot-Ukirde/Autonomous-Mobile-Robot-AMR-Simulation.git

# 2. Install dependencies and build
cd ~/amr_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build --symlink-install
source install/setup.bash
```

## Usage

<!-- TODO: replace the placeholders below with your real package and launch file names. -->

**1. Launch the robot in Gazebo**

```bash
ros2 launch <your_package> <simulation_launch_file>.py
```

**2. Build a map with SLAM**

```bash
ros2 launch <your_package> <slam_launch_file>.py
```

Drive the robot around the environment, then save the map:

```bash
ros2 run nav2_map_server map_saver_cli -f ~/amr_ws/maps/my_map
```

**3. Navigate autonomously**

```bash
ros2 launch <your_package> <navigation_launch_file>.py map:=~/amr_ws/maps/my_map.yaml
```

In RViz2, set the initial pose with **2D Pose Estimate**, then give a goal with **Nav2 Goal**. The robot plans a path and drives there on its own.

## Project structure

<!-- TODO: update this to match your real folders. -->

```
Autonomous-Mobile-Robot-AMR-Simulation/
├── <package_name>/
│   ├── urdf/        # Robot description (URDF/Xacro)
│   ├── launch/      # Simulation, SLAM and navigation launch files
│   ├── config/      # SLAM Toolbox and Nav2 parameters
│   ├── maps/        # Saved occupancy-grid maps
│   ├── worlds/      # Gazebo environments
│   └── rviz/        # RViz2 configurations
└── README.md
```

## Results

<!-- TODO: add screenshots of the map and RViz2 view, and any result you can state truthfully,
e.g. "Reached the goal in X of Y test runs". Leave this section out if you have no result yet. -->

- Screenshot: generated occupancy-grid map
- Screenshot: RViz2 view during navigation

## Limitations

- Tested in simulation only, not on a physical robot.
- Performance depends on the environment, LiDAR settings and tuned Nav2 parameters.

## Future work

- Deploy on a physical differential-drive robot
- Add a camera for vision-based perception
- Test in larger and more complex environments

## Author

**Avdhoot Ukirde**
Robotics and AI, MGM University (JNEC), Chhatrapati Sambhajinagar
GitHub: [@Avdhoot-Ukirde](https://github.com/Avdhoot-Ukirde)
