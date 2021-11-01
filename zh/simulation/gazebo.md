!REDIRECT "https://docs.px4.io/master/zh/simulation/gazebo.html"

# Gazebo 仿真

[ Gazebo ](http://gazebosim.org)是用于自主机器人的强大3D模拟环境，其特别适用于测试物体避障和计算机视觉。 本文描述了如何使用它来进行单机的软件在环仿真。 Gazebo 也可以适用于 [硬件在环仿真](../simulation/hitl.md) 和 [多机仿真](../simulation/multi-vehicle-simulation.md) 。

**支持机型：**四旋翼 （[Iris](../airframes/airframe_reference.md#copter_quadrotor_wide_3dr_iris_quadrotor) 和 [Solo](../airframes/airframe_reference.md#copter_quadrotor_x_3dr_solo)），六旋翼（Typhoon H480），[通用四旋翼构型 VTOL ](../airframes/airframe_reference.md#vtol_standard_vtol_generic_quad_delta_vtol)，尾座式，固定翼，无人车，潜艇/无人水下航行器。

> **Warning** Gazebo 通常与 [ROS](../ros/README.md) 一起使用，ROS 可以理解成 Offboard 自动飞行控制的 API 工具包。 如果您计划同时使用ROS和PX4，则**应遵循**[ ROS说明安装 ](../simulation/ros_interface.md)去安装ROS和Gazebo（从而避免安装冲突）。

{% youtube %}https://www.youtube.com/watch?v=qfFF9-0k4KA&vq=hd720{% endyoutube %}

[![Mermaid Graph: Gazebo plugin](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFI7XG4gIEdhemViby0tPlBsdWdpbjtcbiAgUGx1Z2luLS0-TUFWTGluaztcbiAgTUFWTGluay0tPlNJVEw7IiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggTFI7XG4gIEdhemViby0tPlBsdWdpbjtcbiAgUGx1Z2luLS0-TUFWTGluaztcbiAgTUFWTGluay0tPlNJVEw7IiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

<!-- original graph info
graph LR;
  Gazebo-- >Plugin;
  Plugin-- >MAVLink;
  MAVLink-- >SITL;
-->

> **Note** 有关仿真器、仿真环境和仿真配置（以支持的机型为例）的基本信息，请参见 [仿真 ](/simulation/README.md)。

<a id="installation"></a>

## Installation

Gazebo 9 setup is included in our standard build instructions:

* ** macOS：** [ Mac 上的开发环境](../setup/dev_env_mac.md)。
* **Linux：**Ubuntu LTS/Debian Linux 上安装 Gazebo、 JMAVSim 和 Nuttx（Pixhawk）的开发环境。</li> 
    
    * ** Windows：**暂不支持。</ul> 
    
    Additional installation instructions can be found on [gazebosim.org](http://gazebosim.org/tutorials?cat=guided_b&tut=guided_b1).
    
    ## 运行仿真
    
    Run a simulation by starting PX4 SITL and gazebo with the airframe configuration to load (multicopters, planes, VTOL, optical flow and multi-vehicle simulations are supported).
    
    The easiest way to do this is to open a terminal in the root directory of the PX4 *PX4-Autopilot* repository and call `make` for the desired target. For example, to start a quadrotor simulation (the default):
    
    ```sh
    cd /path/to/PX4-Autopilot
    make px4_sitl gazebo
    ```
    
    The supported vehicles and `make` commands are listed below (click links to see vehicle images).
    
    > **Note** 使用指令 `make px4_sitl list_vmd_make_targets` 获取构建目标的完整列表（并过滤掉以 `gazebo_` 开头的目标）。
    
    | 载具类型                                                                                                | 指令                                     |
    | --------------------------------------------------------------------------------------------------- | -------------------------------------- |
    | [四旋翼](../simulation/gazebo_vehicles.md#quadrotor)                                                   | `make px4_sitl gazebo`                 |
    | [具有光流的四旋翼](../simulation/gazebo_vehicles.md#quadrotor_optical_flow)                                 | `make px4_sitl gazebo_iris_opt_flow`   |
    | [3DR Solo（四旋翼）](../simulation/gazebo_vehicles.md#3dr_solo)                                          | `make px4_sitl gazebo_solo`            |
    | <span id="typhoon_h480"></span>[Typhoon H480（六旋翼）](../simulation/gazebo_vehicles.md#typhoon_h480) （支持视频流） | `make px4_sitl gazebo_typhoon_h480`    |
    | [标准构型的固定翼](../simulation/gazebo_vehicles.md#standard_plane)                                         | `make px4_sitl gazebo_plane`           |
    | [Standard Plane (with catapult launch)](../simulation/gazebo_vehicles.md#standard_plane_catapult)   | `make px4_sitl gazebo_plane_catapult`  |
    | [Standard VTOL](../simulation/gazebo_vehicles.md#standard_vtol)                                     | `make px4_sitl gazebo_standard_vtol`   |
    | [Tailsitter VTOL](../simulation/gazebo_vehicles.md#tailsitter_vtol)                                 | `make px4_sitl gazebo_tailsitter`      |
    | [Ackerman vehicle (UGV/Rover)](../simulation/gazebo_vehicles.md#ugv)                                | `make px4_sitl gazebo_rover`           |
    | [HippoCampus TUHH (UUV: Unmanned Underwater Vehicle)](../simulation/gazebo_vehicles.md#uuv)         | `make px4_sitl gazebo_uuv_hippocampus` |
    | [Boat (USV: Unmanned Surface Vehicle)](../simulation/gazebo_vehicles.md#usv)                        | `make px4_sitl gazebo_boat`            |
    | [Cloudship (Airship)](../simulation/gazebo_vehicles.md#airship)                                     | `make px4_sitl gazebo_cloudship`       |
    
    > **Note** 如果发生构建错误， [文件和代码安装指南](../setup/dev_env.md) 是一个有用的参考。
    
    The commands above launch a single vehicle with the full UI. Other options include:
    
    * 为了使 Gazebo 保持运行，请[分别启动 PX4 和 Gazebo](#start_px4_sim_separately)，并在需要时单独重新启动 PX4（比重新启动两者更快）。
    * 在 [无头模式](#headless) 运行仿真将不会启动 Gazebo UI（使用的资源更少，速度更快）。
    
    ## 让飞行器起飞
    
    The `make` commands above first build PX4, and then run it along with the Gazebo simulator.
    
    Once PX4 has started it will launch the PX4 shell as shown below.
    
        ______  __   __    ___ 
        | ___ \ \ \ / /   /   |
        | |_/ /  \ V /   / /| |
        |  __/   /   \  / /_| |
        | |     / /^\ \ \___  |
        \_|     \/   \/     |_/
        
        px4 starting.
        
        INFO  [px4] Calling startup script: /bin/sh etc/init.d-posix/rcS 0
        INFO  [param] selected parameter default file eeprom/parameters_10016
        [param] Loaded: eeprom/parameters_10016
        INFO  [dataman] Unknown restart, data manager file './dataman' size is 11798680 bytes
        INFO  [simulator] Waiting for simulator to connect on TCP port 4560
        Gazebo multi-robot simulator, version 9.0.0
        Copyright (C) 2012 Open Source Robotics Foundation.
        Released under the Apache 2 License.
        http://gazebosim.org
        ...
        INFO  [ecl/EKF] 5188000: commencing GPS fusion
        
    
    The console will print out status as PX4 loads the airframe-specific initialisation and parameter files, waits for (and connects to) the simulator. Once there is an INFO print that [ecl/EKF] is `commencing GPS fusion` the vehicle is ready to arm.
    
    > **Note** 在 Gazebo 中右击四旋翼模型允许从上下文菜单启用跟随模式，这样可以方便地将其保持在视图中。
    
    ![Gazebo UI](../../assets/simulation/gazebo/gazebo_follow.jpg)
    
    You can bring it into the air by typing:
    
    ```sh
    pxh> commander takeoff
    ```
    
    ## 使用/配置选项
    
    

<a id="headless"></a>

    
    ### Headless Mode
    
    Gazebo can be run in a *headless* mode in which the Gazebo UI is not launched. This starts up more quickly and uses less system resources (i.e. it is a more "lightweight" way to run the simulation).
    
    Simply prefix the normal `make` command with `HEADLESS=1` as shown:
    
    ```bash
    HEADLESS=1 make px4_sitl gazebo_plane
    ```
    
    

<a id="custom_takeoff_location"></a>

    
    ### Set Custom Takeoff Location
    
    The takeoff location in SITL Gazebo can be set using environment variables. This will override both the default takeoff location, and any value [set for the world](#set_world_location).
    
    The variables to set are: `PX4_HOME_LAT`, `PX4_HOME_LON`, and `PX4_HOME_ALT`.
    
    For example:
    
        export PX4_HOME_LAT=28.452386
        export PX4_HOME_LON=-13.867138
        export PX4_HOME_ALT=28.5
        make px4_sitl gazebo
        
    
    ### 更改仿真速率
    
    The simulation speed can be increased or decreased with respect to realtime using the environment variable `PX4_SIM_SPEED_FACTOR`.
    
        export PX4_SIM_SPEED_FACTOR=2
        make px4_sitl_default gazebo
        
    
    For more information see: [Simulation > Run Simulation Faster than Realtime](../simulation/README.md#simulation_speed).
    
    ### Change Wind Speed
    
    To simulate wind speed, add this plugin to your world file and replace `SET_YOUR_WIND_SPEED` with the desired speed:
    
    ```xml
      <plugin name='wind_plugin' filename='libgazebo_wind_plugin.so'>
          <frameId>base_link</frameId>
          <robotNamespace/>
          <xyzOffset>1 0 0</xyzOffset>
          <windDirectionMean>0 1 0</windDirectionMean>
          <windVelocityMean>SET_YOUR_WIND_SPEED</windVelocityMean>
          <windGustDirection>0 0 0</windGustDirection>
          <windGustDuration>0</windGustDuration>
          <windGustStart>0</windGustStart>
          <windGustVelocityMean>0</windGustVelocityMean>
          <windPubTopic>world_wind</windPubTopic>
        </plugin>
    ```
    
    You can see this how this is done in [PX4/PX4-SITL_gazebo/worlds/windy.world](https://github.com/PX4/PX4-SITL_gazebo/blob/master/worlds/windy.world#L15-L26).
    
    ### Using a Joystick
    
    Joystick and thumb-joystick support are supported through *QGroundControl* ([setup instructions here](../simulation/README.md#joystickgamepad-integration)).
    
    ### Improving Distance Sensor Performance
    
    The current default world is [PX4/sitl_gazebo/worlds/**iris.world**](https://github.com/PX4/sitl_gazebo/tree/master/worlds)), which uses a heightmap as ground.
    
    This can cause difficulty when using a distance sensor. If there are unexpected results we recommend you change the model in **iris.model** from `uneven_ground` to `asphalt_plane`.
    
    

<a id="gps_noise"></a>

    
    ### Simulating GPS Noise
    
    Gazebo can simulate GPS noise that is similar to that typically found in real systems (otherwise reported GPS values will be noise-free/perfect). This is useful when working on applications that might be impacted by GPS noise - e.g. precision positioning.
    
    GPS noise is enabled if the target vehicle's SDF file contains a value for the `gpsNoise` element (i.e. it has the line: `<gpsNoise>true</gpsNoise>`). It is enabled by default in many vehicle SDF files: **solo.sdf**, **iris.sdf**, **standard_vtol.sdf**, **delta_wing.sdf**, **plane.sdf**, **typhoon_h480**, **tailsitter.sdf**.
    
    To enable/disable GPS noise:
    
    1. 构建任何 gazebo 目标以生成 SDF 文件（适用于所有机型）。 例如： ```make px4_sitl gazebo_iris``` >**Tip** 在后续版本中不会覆盖 SDF 文件。
    2. 打开目标载具的 SDF 文件（例如**./Tools/sitl_gazebo/models/iris/iris.sdf **）。
    3. 搜索 `gpsNoise` 元素： 
            xml
            <plugin name='gps_plugin' filename='libgazebo_gps_plugin.so'>
             <robotNamespace/>
             <gpsNoise>true</gpsNoise>
            </plugin>
        
        * 如果已预设，则启用 GPS。 您可以通过删除以下行来禁用它：`<gpsNoise> true </gpsNoise>`
        * 如果未预设，则禁用 GPS 。 您可以通过将` gpsNoise `元素添加到` gps_plugin `部分来启用它（如上所示）。
    
    The next time you build/restart Gazebo it will use the new GPS noise setting.
    
    

<a id="set_world"></a>

    
    ## Loading a Specific World
    
    PX4 supports a number of [Gazebo Worlds](../simulation/gazebo_worlds.md), which are stored in [PX4/sitl_gazebo/worlds](https://github.com/PX4/sitl_gazebo/tree/master/worlds)) By default Gazebo displays a flat featureless plane, as defined in [empty.world](https://github.com/PX4/sitl_gazebo/blob/master/worlds/empty.world).
    
    You can load any of the worlds by specifying them as the final option in the PX4 configuration target.
    
    For example, to load the *warehouse* world, you can append it as shown:
    
        make px4_sitl_default gazebo_plane_cam__warehouse
        
    
    > **Note** There are *two underscores* after the model (`plane_cam`) indicating that the default debugger is used (none). 详见 [Building the Code > PX4 Make Build Targets](../setup/building_px4.md#make_targets)。
    
    You can also specify the full path to a world to load using the `PX4_SITL_WORLD` environment variable. This is useful if testing a new world that is not yet included with PX4.
    
    > **Tip** If the loaded world does not align with the map, you may need to [set the world location](#set_world_location).
    
    

<a id="set_world_location"></a>

    
    ## Set World Location
    
    The vehicle gets spawned very close to the origin of the world model at some simulated GPS location.
    
    > **Note** The vehicle is not spawned exactly at the Gazebo origin (0,0,0), but using a slight offset, which can highlight a number of common coding issues.
    
    If using a world that recreates a real location (e.g. a particular airport) this can result in a very obvious mismatch between what is displayed in the simulated world, and what is shown on the ground station map. To overcome this problem you can set the location of the world origin to the GPS co-ordinates where it would be in "real life".
    
    > **Note** You can also set a [Custom Takeoff Location](#custom_takeoff_location) that does the same thing. However adding the location to the map is easier (and can still be over-ridden by setting a custom location if needed).
    
    The location of the world is defined in the **.world** file by specifying the location of the origin using the `spherical_coordinates` tag. The latitude, longitude, elevation must all be specified (for this to be a valid).
    
    An example can be found in the [sonoma_raceway.world](https://github.com/PX4/sitl_gazebo/blob/master/worlds/sonoma_raceway.world):
    
            <spherical_coordinates>
              <surface_model>EARTH_WGS84</surface_model>
              <latitude_deg>38.161479</latitude_deg>
              <longitude_deg>-122.454630</longitude_deg>
              <elevation>488.0</elevation>
            </spherical_coordinates>
        
    
    You can test this by spawning a rover in the [Sonoma Raceway World](../simulation/gazebo_worlds.md#sonoma-raceway) using the following `make` command (note that spawning takes longer the first time as the model needs to be downloaded from the model database):
    
        make px4_sitl gazebo_rover__sonoma_raceway
        
    
    The video below shows that the location of the environment is aligned with the gazebo world: {% youtube %} https://youtu.be/-a2WWLni5do {% endyoutube %}
    
    

<a id="start_px4_sim_separately"></a>

    
    ## Starting Gazebo and PX4 Separately
    
    For extended development sessions it might be more convenient to start Gazebo and PX4 separately or even from within an IDE.
    
    In addition to the existing cmake targets that run `sitl_run.sh` with parameters for px4 to load the correct model it creates a launcher targets named `px4_<mode>` that is a thin wrapper around original sitl px4 app. This thin wrapper simply embeds app arguments like current working directories and the path to the model file.
    
    To start Gazebo and PX4 separately:
    
    * 通过在终端中指定环境变量 `_ide` 来运行 gazebo（或任何其他 sim 卡）服务器和客户端查看器： 
            sh
            make px4_sitl gazebo___ide 或者 
        
            sh
            make px4_sitl gazebo_iris_ide
    
    * 在 IDE 中选择要调试的 `px4_<mode>` 目标（例如 `px4_iris` ）。
    * 直接从 IDE 启动调试会话。
    
    This approach significantly reduces the debug cycle time because simulator (e.g. Gazebo) is always running in background and you only re-run the px4 process which is very light.
    
    ## Simulated Survey Camera
    
    The *Gazebo* survey camera simulates a [MAVLink camera](https://mavlink.io/en/services/camera.html) that captures geotagged JPEG images and sends camera capture information to a connected ground station. The camera also supports video streaming. It can be used to test camera capture, in particular within survey missions.
    
    The camera emits the [CAMERA_IMAGE_CAPTURED](https://mavlink.io/en/messages/common.html#CAMERA_IMAGE_CAPTURED) message every time an image is captured. The captured images are saved to: **PX4-Autopilot/build/px4_sitle_default/tmp/frames/DSC_n_.jpg** (where *n* starts as 00000 and is iterated by one on each capture).
    
    To simulate a plane with this camera:
    
        make px4_sitl_default gazebo_plane_cam
        
    
    > **Note** The camera also supports/responds to the following MAVLink commands: [MAV_CMD_REQUEST_CAMERA_CAPTURE_STATUS](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_CAMERA_CAPTURE_STATUS), [MAV_CMD_REQUEST_STORAGE_INFORMATION](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_STORAGE_INFORMATION), [MAV_CMD_REQUEST_CAMERA_SETTINGS](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_CAMERA_SETTINGS), [MAV_CMD_REQUEST_CAMERA_INFORMATION](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_CAMERA_INFORMATION), [MAV_CMD_RESET_CAMERA_SETTINGS](https://mavlink.io/en/messages/common.html#MAV_CMD_RESET_CAMERA_SETTINGS), [MAV_CMD_STORAGE_FORMAT](https://mavlink.io/en/messages/common.html#MAV_CMD_STORAGE_FORMAT), [MAV_CMD_SET_CAMERA_ZOOM](https://mavlink.io/en/messages/common.html#MAV_CMD_SET_CAMERA_ZOOM), [MAV_CMD_IMAGE_START_CAPTURE](https://mavlink.io/en/messages/common.html#MAV_CMD_IMAGE_START_CAPTURE), [MAV_CMD_IMAGE_STOP_CAPTURE](https://mavlink.io/en/messages/common.html#MAV_CMD_IMAGE_STOP_CAPTURE), [MAV_CMD_REQUEST_VIDEO_STREAM_INFORMATION](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_VIDEO_STREAM_INFORMATION), [MAV_CMD_REQUEST_VIDEO_STREAM_STATUS](https://mavlink.io/en/messages/common.html#MAV_CMD_REQUEST_VIDEO_STREAM_STATUS), [MAV_CMD_SET_CAMERA_MODE](https://mavlink.io/en/messages/common.html#MAV_CMD_SET_CAMERA_MODE).
    
    

<span></span>

    
    > **Note** The simulated camera is implemented in [PX4/sitl_gazebo/src/gazebo_geotagged_images_plugin.cpp](https://github.com/PX4/sitl_gazebo/blob/master/src/gazebo_geotagged_images_plugin.cpp).
    
    

<a id="flight_termination"></a>

    
    ## Simulated Parachute/Flight Termination
    
    *Gazebo* can be used to simulate deploying a [parachute](https://docs.px4.io/master/en/peripherals/parachute.html) during [Flight Termination](https://docs.px4.io/master/en/advanced_config/flight_termination.html) (flight termination is triggered by the PWM command that is simulated in *Gazebo*).
    
    The `if750a` target has a parachute attached to the vehicle. To simulate the vehicle, run the following command:
    
        make px4_sitl gazebo_if750a
        
    
    To put the vehicle into flight termination state, you can force it to fail a [safety check](https://docs.px4.io/master/en/config/safety.html) that has flight termination set as the failsafe action. For example, you could do this by forcing a [Geofence violation](https://docs.px4.io/master/en/config/safety.html#geofence-failsafe).
    
    For more information see:
    
    * [飞行终止](https://docs.px4.io/master/en/advanced_config/flight_termination.html) 
    * [降落伞](https://docs.px4.io/master/en/peripherals/parachute.html)
    * [ 安全配置（故障保护） ](https://docs.px4.io/master/en/config/safety.html)
    
    

<a id="video"></a>

    
    ## Video Streaming
    
    PX4 SITL for Gazebo supports UDP video streaming from a Gazebo camera sensor attached to a vehicle model. When streaming is enabled, you can connect to this stream from *QGroundControl* (on UDP port 5600) and view video of the Gazebo environment from the simulated vehicle - just as you would from a real camera. The video is streamed using a *gstreamer* pipeline and can be enabled/disabled using a button in the Gazebo UI.
    
    The Gazebo camera sensor is supported/enabled on the following frames:
    
    * [Typhoon H480](#typhoon_h480)
    
    ### Prerequisites
    
    *Gstreamer 1.0* is required for video streaming. The required dependencies should already have been [installed when you set up Gazebo](#installation) (they are included in the standard PX4 installation scripts/instructions for macOS and Ubuntu Linux).
    
    > **Note** FYI only, the dependencies include: `gstreamer1.0-plugins-base`, g`streamer1.0-plugins-good`, `gstreamer1.0-plugins-bad`, `gstreamer1.0-plugins-ugly`, `libgstreamer-plugins-base1.0-dev`.
    
    ### Start/Stop Video Streaming
    
    Video streaming is automatically started when supported by the target vehicle. For example, to start streaming video on the Typhoon H480:
    
        make px4_sitl gazebo_typhoon_h480
        
    
    Streaming can be paused/restarted using the Gazebo UI *Video ON/OFF* button..
    
    ![Video ON/OFF button](../../assets/simulation/gazebo/sitl_video_stream.png)
    
    ### How to View Gazebo Video
    
    The easiest way to view the SITL/Gazebo camera video stream is in *QGroundControl*. Simply open **Application Settings > General** and set **Video Source** to *UDP h.264 Video Stream* and **UDP Port** to *5600*:
    
    ![QGC Video Streaming Settings for Gazebo](../../assets/simulation/gazebo/qgc_gazebo_video_stream_udp.png)
    
    The video from Gazebo should then display in *QGroundControl* just as it would from a real camera.
    
    ![QGC Video Streaming Gazebo Example](../../assets/simulation/gazebo/qgc_gazebo_video_stream_typhoon.jpg)
    
    > **Note** The Typhoon world is not very interesting.
    
    It is also possible to view the video using the *Gstreamer Pipeline*. Simply enter the following terminal command:
    
    ```sh
    gst-launch-1.0  -v udpsrc port=5600 caps='application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264' \
    ! rtph264depay ! avdec_h264 ! videoconvert ! autovideosink fps-update-interval=1000 sync=false
    ```
    
    ### Verbose Logging
    
    SITL fails silently when there is something wrong with the gazebo model. You can enable more verbose logging using `VERBOSE_SIM`, as shown:
    
        export VERBOSE_SIM=1
        make px4_sitl gazebo
        
    
    or
    
        VERBOSE_SIM=1 make px4_sitl gazebo
        
    
    ## Extending and Customizing
    
    To extend or customize the simulation interface, edit the files in the `Tools/sitl_gazebo` folder. The code is available on the [sitl_gazebo repository](https://github.com/px4/sitl_gazebo) on Github.
    
    > **Note** The build system enforces the correct GIT submodules, including the simulator. It will not overwrite changes in files in the directory.
    
    ## Further Information
    
    * [ROS 与 Gazebo 仿真](../simulation/ros_interface.md)
    * [Gazebo Octomap](../simulation/gazebo_octomap.md)