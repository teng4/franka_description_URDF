# franka_description_URDF
A package of `franka_description` with URDF files of the Panda robots (fr3, fp3, fer).

## About

This package ["franka_description_URDF"](https://github.com/teng4/franka_description_URDF) is an improved and simplified version based on the original ["franka_description" (official)](https://github.com/frankaemika/franka_description), the main improvements are all related to `URDF` files, including,

- A new `urdfs` folder is newly generated with the `URDF` files inside. For the detailed procedures of generating these URDF files, please see the post ["How To convert [xacro] to [urdf] for Franka Emika Panda robot?"](https://teng4.github.io/posts/20250416/).
- Two `.rviz` files are generated in the folder `rviz` for ROS1 (*noetic, Ubuntu 20.04.6 LTS*).
- For the application of the `URDF` file, please see this [demo video](https://youtu.be/asSwOhIVADU).
- Link to ["franka_description" (teng4)](https://github.com/teng4/franka_description)
- Link to ["franka_description" (official)](https://github.com/frankaemika/franka_description)

## How to use

- Download the package ["franka_description_URDF"](https://github.com/teng4/franka_description_URDF)
- Rename package from `"franka_description_URDF"` to `"franka_description"` (**required**).
- Copy the package `"franka_description"` into a `catkin_ws/src` as an independent package.
- Compile the `catkin_ws` via `catkin_make` (There should be no compiling errors).
- Tested OK on Ubuntu 20.04.6 LTS with ROS noetic.

## Notes

- The original ["franka_description" (official)](https://github.com/frankaemika/franka_description) may have compiling error when run `catkin_make`, that is why this package was created. Therefore, alternatively, you can create your own new package inside your `catkin_ws`, and copy-paste all other folder files into your package.
- You can also copy-paste the folders with the same name from the official ones ["franka_description" (official)](https://github.com/frankaemika/franka_description). Note that folders `rviz` and `urdfs` contain unique files inside that you need to keep in order to show the panda robot in RViz.
- `teng4_dummy.txt` (inside the folders of `meshes` and `include`) was created for the purpose of uploading the files onto GitHub only, you can delete them if they prevent you from compiling the package correctly when running `catkin_make`. Otherwise, you can just leave them unattended.

## Commands to be included in your launch file

```
<launch> 
  <!-- load the controllers -->  
  <node name="omni_panda_cpp" pkg="cleftikpkg" type="omni_panda_cpp" output="screen"> 
  </node>

  <!-- Launch Robot 1 -->
  <group ns="panda1">
    <param name="robot_description" command="cat $(find franka_description)/urdfs/fr3_franka_hand_teng4modified1ok.urdf" /> 
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" />
  </group>

  <node name="rviz" pkg="rviz" type="rviz" args="-d $(find franka_description)/rviz/visualize_franka_teng4modified1ok.rviz" required="true" >
  </node>  
</launch>
```

## Commands to create a new `catkin_ws2`

```
pwd  #Prints the current working directory
echo $ROS_PACKAGE_PATH
source /opt/ros/noetic/setup.bash
mkdir -p ~/catkin_ws2/src
cd ~/catkin_ws2
catkin_make
source devel/setup.bash
echo $ROS_PACKAGE_PATH
```

## Commands to create a new package in `catkin_ws2`

```
pwd  #Prints the current working directory
cd ~/catkin_ws2/src
catkin_create_pkg franka_description std_msgs rospy roscpp
cd ~/catkin_ws2
catkin_make
source devel/setup.bash
echo $ROS_PACKAGE_PATH
```

# Link to Franka Description (official)

Go to the original ["franka_description" (official)](https://github.com/frankaemika/franka_description).


------
Created on 2025-05-01.
