!REDIRECT "https://docs.px4.io/master/zh/SUMMARY.html"

# 概要 

* [简介](README.md)
* [由此开始](setup/getting_started.md) 
  * [初始设置](setup/config_initial.md)
  * [工具链安装](setup/dev_env.md) 
    * [Mac OS](setup/dev_env_mac.md)
    * [Linux](setup/dev_env_linux.md) 
      * [Ubuntu/Debian Linux](setup/dev_env_linux_ubuntu.md)
      * [CentOS Linux](setup/dev_env_linux_centos.md)
      * [Arch Linux](setup/dev_env_linux_arch.md)
      * [高级 Linux](setup/dev_env_advanced_linux.md)
    * [Windows](setup/dev_env_windows.md) 
      * [Cygwin 工具链](setup/dev_env_windows_cygwin.md)
      * [Virtual Machine 工具链](setup/dev_env_windows_vm.md)
      * [Bash on Windows 工具链](setup/dev_env_windows_bash_on_win.md)
    * [Visual Studio Code IDE](setup/vscode.md)
    * [Fast RTPS installation](setup/fast-rtps-installation.md)
    * [Additional Tools](setup/generic_dev_tools.md)
  * [构建代码](setup/building_px4.md)
  * [编写您的第一个应用程序](apps/hello_sky.md)
  * [应用/模块模板](apps/module_template.md)
* [概念](concept/README.md) 
  * [PX4 系统架构概述](concept/architecture.md) 
    * [控制器图解](flight_stack/controller_diagrams.md)
  * [Dronecode 平台概述](concept/dronecode_architecture.md)
  * [飞行模式](concept/flight_modes.md)
  * [Flight Tasks](concept/flight_tasks.md)
  * [Mixing and Actuators](concept/mixing.md) 
    * [Custom Payload Mixer](concept/custom_mixer_payload.md)
  * [PWM limit state machine](concept/pwm_limit.md)
  * [System Startup](concept/system_startup.md)
  * [SD Card Layout](concept/sd_card_layout.md)
* [仿真](simulation/README.md) 
  * [jMAVSim 仿真模拟](simulation/jmavsim.md) 
    * [Multi-Vehicle Sim with JMAVSim](simulation/multi_vehicle_jmavsim.md)
  * [Gazebo 仿真模拟](simulation/gazebo.md) 
    * [Gazebo Vehicles](simulation/gazebo_vehicles.md)
    * [Gazebo Worlds](simulation/gazebo_worlds.md)
  * [Multi-Vehicle Sim with Gazebo](simulation/multi_vehicle_simulation_gazebo.md)
  * [FlightGear Simulation](simulation/flightgear.md) 
    * [FlightGear Vehicles](simulation/flightgear_vehicles.md)
  * [Multi-Vehicle Sim with FlightGear](simulation/multi_vehicle_flightgear.md)
  * [JSBSim Simulation](simulation/jsbsim.md)
  * [AirSim Simulation](simulation/airsim.md)
  * [Multi-Vehicle Simulation](simulation/multi-vehicle-simulation.md)
  * [Simulate Failsafes](simulation/failsafes.md)
  * [HITL Simulation](simulation/hitl.md)
  * [Simulation-In-Hardware](simulation/simulation-in-hardware.md)
* [硬件](hardware/README.md) 
  * [飞行控制器参考设计](hardware/reference_design.md)
  * [Manufacturer’s Board Support Guide](hardware/board_support_guide.md)
  * [Flight Controller Porting Guide](hardware/porting_guide.md) 
    * [NuttX Board Porting Guide](hardware/porting_guide_nuttx.md)
  * [Airframes](airframes/README.md) 
    * [Airframes Reference](airframes/airframe_reference.md)
    * [Adding a New Airframe](airframes/adding_a_new_frame.md)
  * [Device Drivers](middleware/drivers.md)
  * [Telemetry Radio](data_links/telemetry.md) 
    * [SiK Radio](data_links/sik_radio.md)
  * [Sensor and Actuator I/O](sensor_bus/README.md) 
    * [I2C Bus](sensor_bus/i2c.md)
    * [UAVCAN Bus](uavcan/README.md) 
      * [UAVCAN Bootloader](uavcan/bootloader_installation.md)
      * [UAVCAN Firmware Upgrades](uavcan/node_firmware.md)
      * [UAVCAN Configuration](uavcan/node_enumeration.md)
      * [UAVCAN Various Notes](uavcan/notes.md)
    * [UART/Serial Ports](uart/README.md) 
      * [Port-Configurable Serial Drivers](uart/user_configurable_serial_driver.md)
  * [RTK GPS](advanced/rtk_gps.md)
  * [Gimbal \(Mount\) Control Setup](advanced/gimbal_control.md)
  * [Companion Computers](companion_computer/pixhawk_companion.md)
* [中间件](middleware/README.md) 
  * [uORB 消息](middleware/uorb.md)
  * [MAVLink Messaging](middleware/mavlink.md)
  * [RTPS/ROS2 Interface](middleware/micrortps.md) 
    * [Throughput Test](middleware/micrortps_throughput_test.md)
    * [Manually Generate Client/Agent](middleware/micrortps_manual_code_generation.md)
* [模块 & 命令](middleware/modules_main.md) 
  * [命令](middleware/modules_command.md)
  * [通信](middleware/modules_communication.md)
  * [控制器](middleware/modules_controller.md)
  * [驱动](middleware/modules_driver.md) 
    * [Airspeed Sensor](middleware/modules_driver_airspeed_sensor.md)
    * [Baro](middleware/modules_driver_baro.md)
    * [Distance Sensor](middleware/modules_driver_distance_sensor.md)
    * [IMU](middleware/modules_driver_imu.md)
    * [Magnetometer](middleware/modules_driver_magnetometer.md)
  * [估计器](middleware/modules_estimator.md)
  * [Simulations](middleware/modules_simulation.md)
  * [System](middleware/modules_system.md)
  * [Template](middleware/modules_template.md)
* [机器人技术](robotics/README.md) 
  * [Linux 的离板模式控制](ros/offboard_control.md)
  * [ROS](ros/README.md) 
    * [MAVROS \（ROS 上的 MAVLink\）](ros/mavros_installation.md)
    * [MAVROS 离板例程](ros/mavros_offboard.md)
    * [另见 Gazebo 模拟。](simulation/ros_interface.md)
    * [具有 ROS 的 OctoMap 模型](simulation/gazebo_octomap.md)
    * [在 RPi 上安装 ROS](ros/raspberrypi_installation.md)
    * [外部位置估计（基于视觉/运动）](ros/external_position_estimation.md)
    * [Sending Custom Messages from MAVROS](ros/mavros_custom_messages.md)
  * [DroneKit](robotics/dronekit.md)
* [调试日志](debug/README.md) 
  * [常见问题](debug/faq.md)
  * [Consoles/Shells](debug/consoles.md) 
    * [MAVLink Shell](debug/mavlink_shell.md)
    * [System Console](debug/system_console.md)
  * [SWD/JLink Debug Interface](debug/swd_debug.md)
  * [Autopilot Debugging](debug/gdb_debugging.md)
  * [Eclipse/JLink Hardware Debugging](debug/eclipse_jlink.md)
  * [Sensor/Topic Debugging](debug/sensor_uorb_topic_debugging.md)
  * [Simulation Debugging](debug/simulation_debugging.md)
  * [Sending Debug Values](debug/debug_values.md)
  * [System-wide Replay](debug/system_wide_replay.md)
  * [Profiling](debug/profiling.md)
  * [Logging](log/logging.md)
  * [Flight Log Analysis](log/flight_log_analysis.md)
  * [ULog File Format](log/ulog_file_format.md)
* [教程](tutorials/tutorials.md) 
  * [地面控制站](qgc/README.md)
  * [Video Streaming from Odroid C1 to QGC](qgc/video_streaming.md)
  * [远距离视频流](qgc/video_streaming_wifi_broadcast.md)
  * [Connecting an RC Receiver on Linux](tutorials/linux_sbus.md)
* [高级主题](advanced/README.md) 
  * [参数 & 配置](advanced/parameters_and_configurations.md)
  * [参数参照表](advanced/parameter_reference.md)
  * [机器视觉](advanced/computer_vision.md) 
    * [运动捕获（VICON, Optitrack）](tutorials/motion-capture-vicon-optitrack.md)
  * [安装英特尔 RealSense R200 的驱动程序](advanced/realsense_intel_driver.md)
  * [切换状态估计器](advanced/switching_state_estimators.md)
  * [树外模块](advanced/out_of_tree_modules.md)
  * [STM32 Bootloader](software_update/stm32_bootloader.md)
  * [System Tunes](advanced/system_tunes.md)
* [平台测试和 CI](test_and_ci/README.md) 
  * [测试飞行](test_and_ci/test_flights.md) 
    * [测试 MC_01 - 手动模式](test_cards/mc_01_manual_modes.md)
    * [测试 MC_02-完全自主](test_cards/mc_02_full_autonomous.md)
    * [测试 MC_03 - 自动手动混合](test_cards/mc_03_auto_manual_mix.md)
    * [测试 MC_04 -故障安全测试](test_cards/mc_04_failsafe_testing.md)
    * [测试 MC_05-室内飞行（手动模式）](test_cards/mc_05_indoor_flight_manual_modes.md)
  * [单元测试](test_and_ci/unit_tests.md)
  * [持续集成](test_and_ci/continous_integration.md)
  * [Jenkins 持续集成](test_and_ci/jenkins_ci.md)
  * [ROS Integration Testing](test_and_ci/integration_testing.md)
  * [MAVSDK Integration Testing](test_and_ci/integration_testing_mavsdk.md)
  * [Docker Containers](test_and_ci/docker.md)
  * [Maintenance](test_and_ci/maintenance.md)
* [Contribution (&Dev Call)](contribute/README.md) 
  * [Dev Call](contribute/dev_call.md)
  * [Source Code Management](contribute/code.md) 
    * [GIT Examples](contribute/git_examples.md)
  * [Documentation](contribute/docs.md)
  * [Translation](contribute/translation.md)
  * [Terminology/Notation](contribute/notation.md)
  * [Licenses](contribute/licenses.md)
* [Support](contribute/support.md)

## Dronecode 相关资源

* [PX4 用户指南](https://docs.px4.io/master/en/)
* [QGroundControl用户指南](https://docs.qgroundcontrol.com/en/)
* [QGroundControl 开发人员指南](http://dev.qgc.dimianzhan.com/zh/)
* [MAVLink指南](https://mavlink.io/en/)
* [MAVSDK](https://mavsdk.mavlink.io/develop/en/index.html)
* [Dronecode相机管理器](https://camera-manager.dronecode.org/en/)