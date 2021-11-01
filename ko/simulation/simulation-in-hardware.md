!REDIRECT "https://docs.px4.io/master/ko/simulation/simulation-in-hardware.html"

# Simulation-In-Hardware (SIH)

Simulation-In-Hardware (SIH) is an alternative to [Hardware In The Loop simulation (HITL)](../simulation/hitl.md) for a quadrotor. In this setup, everything is running on embedded hardware - the controller, the state estimator, and the simulator. The Desktop computer is only used to display the virtual vehicle.

![Simulator MAVLink API](../../assets/diagrams/SIH_diagram.png)

The SIH provides two benefits over the HITL:

- It ensures synchronous timing by avoiding the bidirectional connection to the computer. As a result the user does not need such a powerful desktop computer.

- The whole simulation remains inside the PX4 environment. Developers who are familiar with PX4 can more easily incorporate their own mathematical model into the simulator. They can, for instance, modify the aerodynamic model, or noise level of the sensors, or even add a sensor to be simulated.

The SIH can be used by new PX4 users to get familiar with PX4 and the different modes and features, and of course to learn to fly a quadrotor with the real RC controller.

동적 모델 설명은 [pdf 보고서](https://github.com/PX4/Devguide/raw/master/assets/simulation/SIH_dynamic_model.pdf)에 있습니다.

Furthermore, the physical parameters representing the vehicle (such as mass, inertia, and maximum thrust force) can easily be modified from the [SIH parameters](../advanced/parameter_reference.md#simulation-in-hardware).

## Requirements

SIH를 실행하려면 [비행체 제어 장치 하드웨어](https://docs.px4.io/master/en/flight_controller/)(예: 픽스호크 시리즈 보드)가 필요합니다. If you are planning to use a [radio control transmitter and receiver pair](https://docs.px4.io/master/en/getting_started/rc_transmitter_receiver.html) you should have that too. Alternatively, using *QGroundControl*, a [joystick](https://docs.qgroundcontrol.com/en/SetupView/Joystick.html) can be used to emulate a radio control system.

The SIH is compatible with all Pixhawk-series boards except those based on FMUv2. It is available on the PX4-Autopilot master branch and release versions v1.9.0 and above.

## Setting up SIH

Running the SIH is as easy as selecting an airframe. Plug the autopilot to the desktop computer with a USB cable, let it boot, then using a ground control station select the [SIH airframe](../airframes/airframe_reference.md#simulation-copter). The autopilot will then reboot.

SIH 에어프레임을 선택하면, SIH 모듈이 자체적으로 시작하고, 기체가 지상 통제 장치의 지도에 떠야합니다.

## Setting up the Display

The simulated quadrotor can be displayed in jMAVSim from PX4 v1.11.

1. *QGroundControl*을 (열었을 경우) 닫으십시오.
2. Unplug and replug the hardware autopilot (allow a few seconds for it to boot).
3. Start jMAVSim by calling the script **jmavsim_run.sh** from a terminal: ```./Tools/jmavsim_run.sh -q -d /dev/ttyACM0 -b 921600 -r 250 -o``` where the flags are 
    - `q`를 누르면 *QGroundControl*와의 통신을 허용합니다(추가).
    - `-d` to start the serial device `/dev/ttyACM0` on Linux. On macOS this would be `/dev/tty.usbmodem1`.
    - `-b` to set the serial baud rate to `921600`.
    - `-r` to set the refresh rate to `250` Hz (optional).
    - `-o` to start jMAVSim in *display Only* mode (i.e. the physical engine is turned off and jMAVSim only displays the trajectory given by the SIH in real-time).
4. 몇 초가 지나면 *QGroundControl*을 다시 열 수 있습니다.

At this point, the system can be armed and flown. The vehicle can be observed moving in jMAVSim, and on the QGC **Fly** view.

## Credits

The SIH was developed by Coriolis g Corporation, a Canadian company developing a new type of Vertical Takeoff and Landing (VTOL) Unmanned Aerial Vehicles (UAV) based on passive coupling systems.

Specialized in dynamics, control, and real-time simulation, they provide the SIH as a simple simulator for quadrotors released for free under BSD license.

Discover their current platform at [www.vogi-vtol.com](http://www.vogi-vtol.com/).