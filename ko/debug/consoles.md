!REDIRECT "https://docs.px4.io/master/ko/debug/consoles.html"

# PX4 콘솔/셸

PX4는 [MAVLink 셸](../debug/mavlink_shell.md)과 [시스템 콘솔](../debug/system_console.md)로 시스템으로의 터미널 접근이 가능합니다.

이 페이지에서는 콘솔/셸 의 차이점과 활용 방법을 설명합니다.

<a id="console_vs_shell"></a>

## System Console vs. Shells

PX4 *시스템 콘솔*은 저수즌 시스템 접근 방식을 제공하며, 디버깅 출력, 시스템 부팅 과정 분석이 가능합니다.

유일한 *시스템 콘솔*은 지정 UART(NuttX에서 설정한 디버깅 포트) 에서만 실행하며, 보통 FTDI 케이블로 컴퓨터에 연결(또는 [드론코드 프로브](https://kb.zubax.com/display/MAINKB/Dronecode+Probe+documentation) 디버깅 어댑터 같은 다른 장비에 붙음)합니다.
- *저수준 디버깅/개발*에 활용: 부팅 과정, NuttX, 시작 스크립트, 보트 부팅, PX4 개발 주요 분야(예: uORB).
- 특히, 모든 부팅 출력(부팅시 프로그램 자동 시작 정보도 해당)이 가능한 부분입니다.

셸에서는 좀 더 고수준의 시스템 접근 수단을 제공합니다:
- 기본 모듈 명령 시험/실행에 활용.
- 실행을 시작한 모듈의 출력을 *직접* 표시함.
- 작업 큐에서 실행하는 작업의 출력은 *직접* 출력할 수 없음.
- 시스템을 시작하지 못하면(실행 상태가 아니기 때문에) 디버깅 문제가 있음.

> **Note** 앞서 가능한 디버깅보다 더 바닥에 가까운 부분의 디버깅이 가능한 `dmesg` 명령은 일부 보드의 셸에서 실행할 수 있습니다. 예를 들면 `dmesg -f &` 명령으로 백그라운드 작업 출력을 볼 수 있습니다.

셸의 종류는 몇가지가 있을 수 있으며 장비에 붙어있는 UART 포트 또는 MAVLink로 실행할수 있습니다. MAVLink로 제공하는 셸이 더 유연하기 때문에 현재는 [MAVLink Shell](../debug/mavlink_shell.md)만 사용합니다.

[시스템 콘솔](../debug/system_console.md)은 시스템이 부팅하지 않을 경우 확인할 핵심적인 부분입니다(보드의 전원을 끊었다가 연결할 때, 시스템 부팅 기록을 표시함). [MAVLink Shell](../debug/mavlink_shell.md)은 설치가 훨씬 쉬우며 대부분의 디버깅 과정에 일반적으로 추천합니다.

<a id="using_the_console"></a>

## Using Consoles/Shells

MAVLink 셸/콘솔과 [시스템 콘솔](../debug/system_console.md)은 상당히 동일한 방식으로 활용합니다.

예를 들어 `ls`를 입력하면 로컬 파일 시스템의 파일과 디렉터리를 볼 수 있고, `free`를 입력하면 남아있는 가용 RAM 용량을 볼 수 있으며, `dmesg`를 입력하면 부팅 출력을 살펴볼 수 있습니다.

```bash
nsh> ls
nsh> free
nsh> dmesg
```

다른 시스템 명령과 모듈은 [모듈 명령 참고](../middleware/modules_main.md)(예: `top`, `listener` 등)에 나와있습니다.

> **Tip** 일부 명령은 어떤 보드에서 사용할 수 없을 때가 있습니다(예: 일부 모듈은 RAM 또는 플래시 용량 제한 때문에 펌웨어에 들어있지 않음). 이 경우 `command not found` 라는 응답을 볼 수 있습니다
