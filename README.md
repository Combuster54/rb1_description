##  Desctiption package
- This package is made on the RB-1 robot https://robotnik.eu/es/productos/robots-moviles/rb-1-base/, it provides all the urdf files and xacro files that describe the robot, controllers and launch files for the gazebo simulation of the RB-1 robot, the controllers loaded in the launch file are joint_state_broadcaster and diff_drive_controller so the robot can be controlled with speed commands. 

- It will also be possible to load the controller for the platform, we leave this up to the user.
    
- Follow the next steps to use the repository in your own workspace
  
![image](https://github.com/Combuster54/rb1_bring_up_controllers/assets/98191055/00e856a5-be3f-4036-adc5-54ded5fbd030)

## Go to your workspace

    cd ~/<your_own_workspace>/src

## Clone the repository in your src directory
    git clone https://github.com/Combuster54/rb1_bring_up_controllers

## Build the package
          
    cd ~/ros2_ws
    colcon build 
    source ~/ros2_ws/install/setup.bash

#  Getting started
## Initialize RB1 robot, differential_drive and up_and_down shelf on Gazebo

    ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py     

Note: your output for each ROS2_controller should be: Sucessfully loaded controller elevator_effort_controller into state active

##  Moving the robot's lifting unit

To move the litting unit, it must be published in the topic "/elevator_effort_controller/commands" as follows:
- UP

        ros2 topic pub /elevator_effort_controller/commands  std_msgs/msg/Float64MultiArray "{data: [10.0]}" -1
        
    ![up](https://github.com/Combuster54/rb1_bring_up_controllers/assets/98191055/0e2b07af-504f-417e-baff-d5da4a4db28d)

- DOWN


        ros2 topic pub /elevator_effort_controller/commands  std_msgs/msg/Float64MultiArray "{data: [0.0]}" -1


    ![down](https://github.com/Combuster54/rb1_bring_up_controllers/assets/98191055/7126c5fc-b3df-40f1-9b1d-559c371302ed)


## Finally, you can send velocity commands with this command:

- MOVE


      ros2 topic pub --rate 10 /rb1_base_controller/cmd_vel_unstamped geometry_msgs/msg/Twist "{linear: {x: 0.2, y: 0, z: 0.0}, angular: {x: 0.0,y: 0.0, z: 0.2}}"


    ![move](https://github.com/Combuster54/rb1_bring_up_controllers/assets/98191055/3ed6896f-f86c-4624-835d-9721d2e4b2d3)

 