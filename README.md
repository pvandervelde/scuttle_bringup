# scuttle_bringup

Provides a convenient entrypoint for starting all the SCUTTLE related ROS nodes in the correct order.

## Dependencies


The configurations in this repository assume you have the following prerequisites installed on the
device on which you want to run this code. That device might be an Ubuntu machine or a physical
SCUTTLE using Raspberry Pi OS.

1. [ROS Noetic](http://wiki.ros.org/noetic) with the `ros-noetic-navigation`, `ros-noetic-robot` and
   `ros-noetic-tf2` packages.
1. A working [ROS workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace).
1. The [scuttle_navigation](https://github.com/scuttlerobot/scuttle_navigation) package should be
   installed.
1. If launched on a physical SCUTTLE then the [scuttle_driver](https://github.com/scuttlerobot/scuttle_driver)
   package should be installed.
1. If launched via a [systemd daemon](https://en.wikipedia.org/wiki/Systemd) then the
   [teleop_twist_joy](https://github.com/scuttlerobot/teleop_twist_joy) package should be installed.

*Note:* `scuttle_bringup` does not launch [scuttle_slam](https://github.com/scuttlerobot/scuttle_slam)
by default because not all SCUTTLE robots come equipped with a LIDAR. Additionally the implementation
of the [Gmapping](http://wiki.ros.org/gmapping) algorithm outputs a large amount of logs to the console
that cannot be silenced easily. It is more appropriate to run this node separately and suppress the
logs when they are not needed.

## Usage

There are two different ways to launch `scuttle_bringup` depending on the reason for launching
the SCUTTLE ROS nodes.

When launching the SCUTTLE ROS nodes manually it is recommended to use the
[launch/scuttle_bringup.launch](launch/scuttle_bringup.launch) file as follows

    roslaunch scuttle_bringup scuttle_bringup.launch

This will launch all the required nodes for navigation with SCUTTLE using ROS.

When launching the SCUTTLE ROS nodes as part of the start-up process of a physical scuttle you can
use the [launch/scuttle_bringup_daemon.launch](launch/scuttle_bringup_daemon.launch) file. This
will launch the navigation stack as well as an additional node for joystick control so that you can
control the SCUTTLE with the provided joypad.
