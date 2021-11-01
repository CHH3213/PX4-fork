!REDIRECT "https://docs.px4.io/master/ko/debug/system_console.html"

# PX4 시스템 콘솔

PX4 *시스템 콘솔*에서는 시스템 저수준 접근이 가능하며, 디버깅 출력과 시스템 부팅 과정 분석을 진행할 수 있습니다.

> **Tip** 시스템이 부팅하지 않는지 디버깅하려면 콘솔을 사용해야합니다. [MAVLink 셸](../debug/mavlink_shell.md)은 아마도 설치하기 쉽고 [동일한 여러 작업 처리](../debug/consoles.md#console_vs_shell)에 활용할 수 있기에 다용도로 적격이라 봅니다.

## 콘솔 연결

콘솔은 [3.3V FTDI](https://www.digikey.com/product-detail/en/TTL-232R-3V3/768-1015-ND/1836393) 케이블을 활용하여 컴퓨터에 USB 포트를 연결할 수 있게 하는 (보드별) UART 포트로 띄울 수 있습니다. 이 포트는 터미널 프로그램으로 콘솔에 접근할 수 있게 해줍니다.

픽스호크 컨트롤러 제조사는 [픽스호크 커넥터 표준](#pixhawk_debug_port)을 준수하는 내장 *디버깅 포트*로 콘솔 UART와 SWD(JTAG) 디버깅 인터페이스를 장치 외부로 제공하리라 봅니다. 그러나 불행하게도 일부 보드는 이 표준을 제정하기 이전의 설계를 반영했거나, 호환성이 없습니다.

> **Tip** 여러가지 보드를 대상으로 개발하려는 개발자는 아마도 여러 보드에 간단하게 연결하는 *디버깅 어댑터* 활용하는 편을 원할지도 모릅니다. 이를테면, [드론코드 프루브](https://kb.zubax.com/display/MAINKB/Dronecode+Probe+documentation)에는 [픽스호크 디버깅 포트](#pixhawk_debug_port)와 여러 기타 보드에 활용할 커넥터가 딸려옵니다.

아래 절에서는 여러 보드에서 활용할 결선 개요 및 시스템 콘솔 정보를 다루겠습니다.

### 보드별 연결 방법

시스템 콘솔 UART 핀 출력/디버깅 포트는 [오토파일럿 개요 페이지](https://docs.px4.io/master/en/flight_controller/)에 정리해두었습니다(아래 링크에 있음):

- [3DR 픽스호크 v1 비행체 제어 장치](https://docs.px4.io/master/en/flight_controller/pixhawk.html#console-port) ([mRo 픽스호크](https://docs.px4.io/master/en/flight_controller/mro_pixhawk.html#debug-ports), [하비킹 HKPilot32](https://docs.px4.io/master/en/flight_controller/HKPilot32.html#debug-port)에도 적용)
- [픽스호크 3](https://docs.px4.io/master/en/flight_controller/pixhawk3_pro.html#debug-port)
- [픽스레이서](https://docs.px4.io/master/en/flight_controller/pixracer.html#debug-port)

- [스냅드래곤 플라이트](https://docs.px4.io/master/en/flight_controller/snapdragon_flight.html):
  
  - [FTDI](https://docs.px4.io/master/en/flight_controller/snapdragon_flight_advanced.html#over-ftdi)
  - [DSP 디버깅 모니터/콘솔](https://docs.px4.io/master/en/flight_controller/snapdragon_flight_advanced.html#dsp-debug-monitorconsole)

<a id="pixhawk_debug_port"></a>

### Pixhawk Debug Port

Flight controllers that adhere to the Pixhawk Connector standard use the [Pixhawk Standard Debug Port](https://pixhawk.org/pixhawk-connector-standard/#dronecode_debug).

The port/FTDI mapping is shown below.

| 픽스호크 디버깅 포트 | -                        | FTDI | -                        |
| ----------- | ------------------------ | ---- | ------------------------ |
| 1 (적)       | TARGET PROCESSOR VOLTAGE |      | 연결 안함 (SWD/JTAG 디버깅에 활용) |
| 2 (흑)       | CONSOLE TX (출력)          | 5    | FTDI RX (황)              |
| 3 (흑)       | CONSOLE RX (입력)          | 4    | FTDI TX (주황)             |
| 4 (흑)       | SWDIO                    |      | 연결 안함 (SWD/JTAG 디버깅에 활용) |
| 5 (흑)       | SWCLK                    |      | 연결 안함 (SWD/JTAG 디버깅에 활용) |
| 6 (흑)       | GND                      | 1    | FTDI GND (흑)             |

## 콘솔 열기

After the console connection is wired up, use the default serial port tool of your choice or the defaults described below:

### Linux / Mac OS: Screen

Install screen on Ubuntu (Mac OS already has it installed):

```bash
sudo apt-get install screen
```

- 직렬 포트: 픽스호크 v1 / 픽스레이서 전송율: 57600 bps
- 직렬 포트: 스냅드래곤 플라이트의 경우 115200 bps

Connect screen at BAUDRATE baud, 8 data bits, 1 stop bit to the right serial port (use `ls /dev/tty*` and watch what changes when unplugging / replugging the USB device). Common names are `/dev/ttyUSB0` and `/dev/ttyACM0` for Linux and `/dev/tty.usbserial-ABCBD` for Mac OS.

```bash
screen /dev/ttyXXX BAUDRATE 8N1
```

### 윈도우: PuTTY

Download [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) and start it.

Then select 'serial connection' and set the port parameters to:

- 초당 전송 비트: 57600
- 데이터 비트: 8
- 정지 비트: 1