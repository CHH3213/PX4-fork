!REDIRECT "https://docs.px4.io/master/zh/dev_setup/dev_env.html"

# Setting up a Developer Environment (Toolchain)

PX4 code can be developed on [Linux](../setup/dev_env_linux.md), [Mac OS](../setup/dev_env_mac.md), or [Windows](../setup/dev_env_windows.md). 我们建议使用 [Ubuntu Linux LTS edition](https://wiki.ubuntu.com/LTS) ，因为它支持编译 [所有 PX4 平台](#supported-targets) 的固件，且可以使用 [ROS](../ros/README.md) 和大部分的 [模拟器](../simulation/README.md) 。

## 支持的编译目标

下表显示了您可以在每个操作系统上构建何种 PX平台的固件编译。

| 平台                                                                                                                                                                                                                                                                                               | Linux (Ubuntu) | Mac | Windows |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |:--------------:|:---:|:-------:|
| **NuttX based hardware:** [Pixhawk Series](https://docs.px4.io/master/en/flight_controller/pixhawk_series.html), [Crazyflie](https://docs.px4.io/master/en/flight_controller/crazyflie2.html), [Intel® Aero Ready to Fly Drone](https://docs.px4.io/master/en/flight_controller/intel_aero.html) |       X        |  X  |    X    |
| [Qualcomm Snapdragon Flight hardware](https://docs.px4.io/master/en/flight_controller/snapdragon_flight.html)                                                                                                                                                                                    |       X        |     |         |
| **Linux-based hardware:** [Raspberry Pi 2/3](https://docs.px4.io/master/en/flight_controller/raspberry_pi_navio2.html)                                                                                                                                                                           |       X        |     |         |
| **模拟器：** [jMAVSim SITL](../simulation/jmavsim.md)                                                                                                                                                                                                                                                |       X        |  X  |    X    |
| **模拟器：** [Gazebo SITL](../simulation/gazebo.md)                                                                                                                                                                                                                                                  |       X        |  X  |         |
| **模拟器：** [ROS with Gazebo](../simulation/ros_interface.md)                                                                                                                                                                                                                                       |       X        |     |         |

## 开发环境

不同操作系统的开发环境的安装请参阅：

- [Mac OS](../setup/dev_env_mac.md)
- [Linux](../setup/dev_env_linux.md)
- [Windows](../setup/dev_env_windows.md)

如果你对 Docker 比较熟悉的话你也可以使用预先构建好的容器作为开发环境：[Docker 容器](../test_and_ci/docker.md)。