!REDIRECT "https://docs.px4.io/master/ko/test_and_ci/test_flights.html"

# 시험 비행

시험 비행은 품질 보증에 중요한 과정입니다. 드론코드 시험 팀에서는 여러분이 보낸 pull 요청의 검토(시험 비행)를 지원할 수 있고 기록에 대한 의견을 제시할 수 있습니다.

{% if book.px4_version != 'master' %}

> **Tip** 시험 비행 절차와 시험 비행대 정보는 매번 바뀔 수 있습니다. 현재 정보는 [head 리비전/master 문서에서 찾을 수 있습니다](https://dev.px4.io/master/en/test_and_ci/test_flights.html)! {% else %} <!-- START: details below displayed only in master -->

## 시험 비행 요청 방법

* 여러분이 바꾼 코드를 pull 요청에 추가하십시오
* **@PX4/testflight** 태그로 댓글에 시험 팀을 호출하십시오 
* 시험 팀의 답변을 기다리십시오
* The test team will [add your PR/issue to their queue](https://github.com/PX4/PX4-Autopilot/projects/18)

## 응답 시간

* 멀티콥터: 최대 48시간(보통 24시간 이내)
* 수직이착륙기, 고정익: 최대 4일(보통 2일)

## 시험 항목

각 플랫폼을 대상으로 수행할 시험은 아래 링크와 같습니다:

* [MC_01 - 수동 상태](../test_cards/mc_01_manual_modes.md)
* [MC_02 - 완전 자동화](../test_cards/mc_02_full_autonomous.md)
* [MC_03 - 자동 / 수동 혼합](../test_cards/mc_03_auto_manual_mix.md)
* [MC_04 - 안전 장치 시험](../test_cards/mc_04_failsafe_testing.md)
* [MC_05 - 실내 비행 (수동 상태)](../test_cards/mc_05_indoor_flight_manual_modes.md)

<a id="fleet"></a>

## Test Vehicles/Autopilots

Multicopter

| 프레임                                                                                                                                                                                                                                                               | 비행체 제어 장치                                                                                                                                                                                                                                                        | UUID                                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhawk Mini](https://docs.px4.io/master/en/flight_controller/pixhawk_mini.html)                                                                                                                                                                                | 002400283335510A33373538 (f450-v3)                          |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhawk 1](https://docs.px4.io/master/en/flight_controller/pixhawk.html)                                                                                                                                                                                        | 000100000000363533353336510900500021 (f450-v3)              |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Cube](https://docs.px4.io/master/en/flight_controller/pixhawk-2.html) (픽스호크 2.1)                                                                                                                                                                                | 00010000000033343537313751050040001c (F450 Pixhawk v2 cube) |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixracer](https://docs.px4.io/master/en/flight_controller/pixracer.html)                                                                                                                                                                                        | 00010000000037373430333551170037002a (F450-Pixracer)        |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhawk 3 Pro](https://docs.px4.io/master/en/flight_controller/pixhawk3_pro.html)                                                                                                                                                                               | 000100000000303236353136510500180036 (Pixhawk pro)          |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhack V3](https://docs.px4.io/master/en/flight_controller/pixhack_v3.html)                                                                                                                                                                                    | 003200293036511638363834 (f450-v5-m)                        |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhawk 4](https://docs.px4.io/master/en/flight_controller/pixhawk4.html)                                                                                                                                                                                       | 000200000000383339333038510700320016 (F450-v5)              |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html)                                                                                                                                                                                             | [Pixhawk 4 Mini](https://docs.px4.io/master/en/flight_controller/pixhawk4_mini.html)                                                                                                                                                                             | 0002000000003432333830385115003a0033 (F450-v5-m)            |
| [DJI F450](https://www.getfpv.com/dji-flamewheel-f450-basic-kit.html) [UAVCAN](https://zubax.com/technologies/uavcan)                                                                                                                                             | [Pixhawk 4](https://docs.px4.io/master/en/flight_controller/pixhawk4.html)                                                                                                                                                                                       | 000200000000323634353237511800200021 (F450-Pixhawk4)        |
| Holybro [QAV250](https://docs.px4.io/master/en/frames_multicopter/holybro_qav250_pixhawk4_mini.html)                                                                                                                                                              | [Pixhawk 4 Mini](https://docs.px4.io/master/en/flight_controller/pixhawk4_mini.html)                                                                                                                                                                             | 000200000000343233383038511500420032 (f450-v5-m)            |
| NXP Semiconductor [KIT-HGDRONEK66](https://www.nxp.com/applications/solutions/industrial/unmanned-aerial-vehicles-uavs/uavs-drones-and-rovers/rddrone-fmuk66-px4-robotic-drone-fmu-reference-design:RDDRONE-FMUK66) ("[Hovergames](https://www.hovergames.com/)") | [RDDRONE-FMUK66](https://www.nxp.com/products/processors-and-microcontrollers/arm-based-processors-and-mcus/kinetis-cortex-m-mcus/k-seriesperformancem4/k6x-ethernet/rddrone-fmuk66-px4-robotic-drone-fmu-reference-design:RDDRONE-FMUK66?tid=vanRDDRONE-FMUK66) | 00030016ffffffffffff4e45362050130029                        |

Fixed Wing

| 프레임                                                                                                 | 비행체 제어 장치                                                                 | UUID                                           |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ---------------------------------------------- |
| [Phantom Wing](https://hobbyking.com/en_us/phantom-fpv-flying-wing-epo-airplane-1550mm-v2-kit.html) | [Pixhawk 1](https://docs.px4.io/master/en/flight_controller/pixhawk.html) | 0001000000003035333330365104003c0020 (f450-v2) |

VTOL

| 프레임                                                                            | 비행체 제어 장치                                                                            | UUID                                             |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------ |
| [혼합 수직 이착륙기](https://www.horizonhobby.com/convergence-vtol-bnf-basic-efl11050) | [Pixhawk 4 Mini](https://docs.px4.io/master/en/flight_controller/pixhawk4_mini.html) | 000200000000343233383038511500350039 (vtol-v5-m) |
| [Delta Quad Pro](https://px4.io/portfolio/deltaquad-vtol/)                     | [Dropix](https://docs.px4.io/master/en/flight_controller/dropix.html)                | 0001000000003437393931375114004c0042 (delta-v2)  |

{% endif %} <!-- END: details above displayed only in master -->