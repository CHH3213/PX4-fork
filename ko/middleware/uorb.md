!REDIRECT "https://docs.px4.io/master/ko/middleware/uorb.html"

# uORB 메시징

## 소개

uORB는 스레드간/프로세스간 통신을 위해 사용되는 비동기 Pub/Sub 메시징 API입니다.

C++에서 어떻게 사용하는지는 [여기](../apps/hello_sky.md)를 봐주세요.

uORB는 많은 어플리케이션이 의존하고 있기 때문에 부트업시에 자동적으로 시작됩니다. `uorb start` 로 시작됩니다. 단위 테스트는 `uorb_tests`를 통해 수행할 수 있습니다.

## 새로운 토픽 추가하기

New uORB topics can be added either within the main PX4/PX4-Autopilot repository, or can be added in an out-of-tree message definitions. 독립적인 브랜치에 uORB 메시지 정의에 추가하는 것은 [이 섹션](../advanced/out_of_tree_modules.md#uorb_message_definitions)을 참고하세요.

새로운 토픽을 만들기 위해서는 `msg/` 디렉토리에 **.msg** 파일을 만들고 `msg/CMakeLists.txt` 리스트에 추가해야합니다. 필요한 C/C++ 코드는 자동적으로 생성됩니다.

지원되는 타입들을 확인하기 위해서는 이미있는 `msg` 파일들을 살펴보세요. 하나의 메시지는 다른 메시지에 포함될 수도 있습니다.

생성된 C/C++ 구조체에는 `uint64_t timestamp` 필드가 추가됩니다. 로깅을 위해 사용되며 메시지를 퍼블리시할때 설정해줘야 합니다.

만든 토픽을 사용하기 위해서는 헤더를 포함해야합니다.

    #include <uORB/topics/topic_name.h>
    

`.msg` 파일에 한줄을 추가함으로써, 하나의 메시지 정의를 다수의 독립된 토픽들을 위해 사용할 수 있습니다.

    # TOPICS mission offboard_mission onboard_mission
    

그리고 소스코드에서 토픽 ID `ORB_ID(offboard_mission)`로 사용하세요.

## 퍼블리시

토픽을 퍼블리싱하는 것은 인터럽트 컨텐스를 포함하는 어느 시스템의 어디에서나 수행할 수 있습니다( `hrt_call` API에 의해 호출됨). 그러나, 토픽을 advertising 하는 것은 인터럽트 컨텍스트의 외부에서만 가능합니다. 토픽을 나중에 퍼블리시할때와 동일한 프로세스에서 Advertise 해야합니다.

## 토픽 리스팅과 리스닝

> **Note** `listener` 명령어는 Pixracer(FMUv4)와 Linux / OS X 에서만 사용가능 합니다.

모든 토픽을 리스팅하기 위해서는 파일 핸들들을 리스팅해야 합니다.

```sh
ls /obj
```

5개의 메시지에 대해 하나의 토픽에 대한 컨텐츠를 수신하고 싶다면,

```sh
listener sensor_accel 5
```

출력은 토픽 내용의 n배 입니다.

```sh
TOPIC: sensor_accel #3
timestamp: 84978861
integral_dt: 4044
error_count: 0
x: -1
y: 2
z: 100
x_integral: -0
y_integral: 0
z_integral: 0
temperature: 46
range_m_s2: 78
scaling: 0

TOPIC: sensor_accel #4
timestamp: 85010833
integral_dt: 3980
error_count: 0
x: -1
y: 2
z: 100
x_integral: -0
y_integral: 0
z_integral: 0
temperature: 46
range_m_s2: 78
scaling: 0
```

> **Tip** NuttX기반의 시스템(Pixhawk, Pixracer 등)에서는 *QGroundControl* MAVLink 콘솔에서 센서 값과 다른 토픽들을 검사하려 `listener` 명령을 호출할 수 있습니다. 이 방법은 QGC가 무선으로 연결되어 있을 때 (예. 비행 중 일때)에도 사용할 수 있기 때문에 강력한 디버깅 툴입니다. 더 많은 정보는 [Sensor/Topic Debugging](../debug/sensor_uorb_topic_debugging.md)를 참고하세요.

### uorb top Command

`uorb top` 명령어는 각 토픽의 전송 주기를 실시간으로 보여줍니다.

```sh
update: 1s, num topics: 77
TOPIC NAME                        INST #SUB #MSG #LOST #QSIZE
actuator_armed                       0    6    4     0 1
actuator_controls_0                  0    7  242  1044 1
battery_status                       0    6  500  2694 1
commander_state                      0    1   98    89 1
control_state                        0    4  242   433 1
ekf2_innovations                     0    1  242   223 1
ekf2_timestamps                      0    1  242    23 1
estimator_status                     0    3  242   488 1
mc_att_ctrl_status                   0    0  242     0 1
sensor_accel                         0    1  242     0 1
sensor_accel                         1    1  249    43 1
sensor_baro                          0    1   42     0 1
sensor_combined                      0    6  242   636 1
```

각 컬럼의 내용은 토픽 이름, 다중 인스턴스 색인 번호, 지속 수신자 수, Hz 단위 송신 빈도, 초당 손실 메세지 수(모든 지속 수신자 통합), 큐 용량입니다.

## 다중 인스턴스

uORB는 `orb_advertise_multi`로 동일 토픽의 다중 독립 인스턴스를 내보내는 매커니즘을 제공합니다. 이 메커니즘은 송신자에게 인스턴스의 색인 번호를 반환합니다. 그러면 지속 수신자는 `orb_subscribe_multi`로 (`orb_instance`는 처음 인스턴스를 지속 수신) 어떤 인스턴스의 메세지를 지속적으로 수신할 지 선택합니다. 다중 인스턴스 보유는 시스템에 동일한 형식의 센서 여러개가 있을 때 도움이 될 수 있습니다.

같은 토픽에서 `orb_advertise_multi`과 `orb_advertise`가 섞이지 않도록 유의하십시오.

The full API is documented in [src/modules/uORB/uORBManager.hpp](https://github.com/PX4/PX4-Autopilot/blob/master/src/modules/uORB/uORBManager.hpp).

<a id="deprecation"></a>

## Message/Field Deprecation

As there are external tools using uORB messages from log files, such as [Flight Review](https://github.com/PX4/flight_review), certain aspects need to be considered when updating existing messages:

- 업데이트상 타당한 이유가 있을 경우에는 기존 필드와 외부 도구에 의존하는 메세지를 바꾸는게 일반적으로 통용됩니다. 특히 *Flight Review*에서 바뀐 내용을 깼을 경우, `master`에 코드를 병합하기 전에 *Flight Review*를 업데이트해야합니다.
- 외부 도구로 두 메세지 버전간 구분을 확실히 하려면 다음 과정을 따라야합니다: 
  - Removed or renamed messages must be added to the `deprecated_msgs` list in [msg/CMakeLists.txt](https://github.com/PX4/PX4-Autopilot/blob/master/msg/CMakeLists.txt#L157) and the **.msg** file needs to be deleted.
  - 제거했거나 삭제한 필드는 주석처리하고 지원 중단(deprecated) 표시합니다. 예를 들면 `uint8 quat_reset_counter`는 `# DEPRECATED: uint8 quat_reset_counter`로 바꿉니다. 이렇게 하면 앞으로 제거한 필드(또는 메세지)를 다시 추가하면 안되겠구나 하고 확인할 수 있습니다.
  - 문맥적으로 바뀌었을 경우(예: 도에서 라디안으로 각 단위가 바뀌었을 때), 해당 필드 역시 이름을 바꾸고 앞서 활용한 필드는 위에서와 같이 지원 중단(deprecated) 표시합니다.