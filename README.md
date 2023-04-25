# Robotics_Phase_3
**This repository contains the code changes for Lab 7 and is the final implementation of Phase 3**

## Tools Utilized
* ROS
* Docker
* Git
* Gazebo
* ur5e robotic arm
* Intel RealSense RGBD Camera

## Package Dependencies
1. ur5e_control package
2. robot_vision_lectures

## Checklist
1. Run `roscore`
2. Connect to the robot
    * For Simulator:
        * `roslaunch ur_gazebo ur5e_bringup.launch`
    * Real Robot:
        * `rosrun ur5e_control ur5e_ros_connection.sh`
3. **IF IN SIMULATOR:** Initialize robot
    * `rosrun robotics_phase3 lawson_init_p3.py`
        * **Stop node execution after robot reaches desired initial configuration**
4. Run Robot Controller
    *  `roslaunch ur5e_control ur5e_controller.launch`
5. Launch frame publisher
    * `roslaunch ur5e_control frame_publisher.launch`
6. Run trajectory generator
    * For Simulator:
        * `rosrun ur5e_control task_space_traj`
    * Real Robot:
        * `rosrun ur5e_control task_space_traj_gripper`
7. Get Camera data
    * For Simulator:
        1. cd Downloads/
        2. ./play_data.sh
    * Real Robot:
        * `roslaunch realsense2_camera rs_rgbd.launch`
8. Open `robot_ball.rviz` in `RVIZ`
    * Visualize ball detection and model fitting
9. Run 2D ball detection
    *  `rosrun robotics_phase3 lawson_p3_detect_ball.py`
10. Run 3D ball detection
    * `rosrun robot_vision_lectures crop_visualize_3D`
11. Run sphere fitting
    * `rosrun robotics_phase3 lawson_p3_sphere_fit.py`
12. Run planner
    * `rosrun robotics_phase3 lawson_phase3.py`
13. Run `rqt_gui` for publishing to available Boolean topics
    1. `rosrun rqt_gui rqt_gui`
    2. Open topics for:
        * `/movement` (True: Robot Holds Movement, False: Robot Moves)
        * `/pause_tracking` (True: `lawson_p3_sphere_fit.py` stops publishing sphere parameters)
        * `/generate_plan` (True: `lawson_phase3.py` will generate a new plan)
14. Look at the sphere model in the open `RVIZ` window
    * **IF the model has converged to a safe point:**
        * Publish a value of **TRUE** to `/pause_tracking` in `rqt_gui`
15. Review generated plan in terminal running the `lawson_phase3.py` node
    * **Avoid negative x values**
    * **Ensure the Z axis values for the pickup and drop off points are above 2cm**
    * **IF THE PLAN IS NOT SATISFACTORY:**
        1. Unpause ball tracking
            * Publish a value of **FALSE** to `/pause_tracking` in `rqt_gui`
        2. Publish a value of **TRUE** to `/generate_plan` in `rqt_gui`
        3. Repeat checklist process starting from step 14.
    * **IF THE PLAN IS SATISFACTORY:**
        * Publish a value of **FALSE** to `/movement` to begin executing the plan
            
