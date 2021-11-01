!REDIRECT "https://docs.px4.io/master/zh/apps/hello_sky.html"

# 搭建你的第一个应用（Hello Shy）

本文主要说明如何创建并运行你的第一个板载应用程序。 它涵盖了 PX4 应用程序开发所需的所有基本概念和 API。

> **Note** 简单起见，这里略过了功能的开启/关闭、命令行参数等更高级的特性。 这些内容将会在 [Application/Module Template](../apps/module_template.md) 中进行介绍。

## 系统必备组件

你需要具备如下组件：

* [PX4 SITL Simulator](../simulation/README.md) *or* a [PX4-compatible flight controller](https://docs.px4.io/master/en/flight_controller/#documented-boards).
* 适用于期望平台的 [PX4 开发工具链](../setup/dev_env.md) 。
* 从 Github [下载 PX4 源代码](../setup/building_px4.md#get_px4_code) 。

The source code [PX4-Autopilot/src/examples/px4_simple_app](https://github.com/PX4/PX4-Autopilot/tree/master/src/examples/px4_simple_app) directory contains a completed version of this tutorial that you can review if you get stuck.

* 重命名 (或删除) **px4_simple_app** 目录。 

## 最小的应用程序

在本节中, 我们将创建一个仅打印出 `Hello Sky!` 的 *最小应用程序* 。 该程序由一个 *C* 和一个 *cmake* 定义文件（该定义文件负责告诉工具链应该如何编译应用程序）组成。

1. Create a new directory **PX4-Autopilot/src/examples/px4_simple_app**.
2. 在该目录中新建一个名为 **px4_simple_app.c** 的 C 文件：

* 将下面的默认头部注释复制到文件页面的顶部， 该注释应出现在所有贡献的文件中！
    
    ```c /**************************************************************************** *
    
    * Copyright (c) 2012-2019 PX4 Development Team. All rights reserved.
    * 
    * Redistribution and use in source and binary forms, with or without
    * modification, are permitted provided that the following conditions
    * are met:
    * 
    * 1. Redistributions of source code must retain the above copyright
    * notice, this list of conditions and the following disclaimer.
    * 2. Redistributions in binary form must reproduce the above copyright
    * notice, this list of conditions and the following disclaimer in
    * the documentation and/or other materials provided with the
    * distribution.
    * 3. Neither the name PX4 nor the names of its contributors may be
    * used to endorse or promote products derived from this software
    * without specific prior written permission.
    * 
    * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    * "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    * LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
    * FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
    * COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
    * INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
    * BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
    * OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
    * AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
    * LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
    * ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
    * POSSIBILITY OF SUCH DAMAGE.
    * ****************************************************************************/ ```

* 将下面的代码复制到头部注释的下方， This should be present in all contributed files!
    
    ```c /**
    
    * @file px4_simple_app.c
    * Minimal application example for PX4 autopilot
    * 
    * @author Example User [&#x6d;&#97;&#105;l&#x40;&#x65;&#120;&#97;&#109;&#x70;&#x6c;&#x65;&#46;&#99;o&#x6d;](&#x6d;&#x61;&#105;&#108;&#116;&#x6f;&#x3a;&#x6d;&#97;&#105;l&#x40;&#x65;&#120;&#97;&#109;&#x70;&#x6c;&#x65;&#46;&#99;o&#x6d;) */
        
        # include <px4_platform_common>
        
        __EXPORT int px4_simple_app_main(int argc, char *argv[]);
        
        int px4_simple_app_main(int argc, char *argv[]) { PX4_INFO("Hello Sky!"); return OK; } ```
        
        > **Tip** 主函数必须跟上述代码一样以 `<module_name>_main` 的形式进行命名并完成从模块中导出。
        
        <span></span>
        
        > **Tip** `PX4_INFO` is the equivalent of `printf` for the PX4 shell (included from **px4_platform_common/log.h**). 有以下不同的日志级别： `PX4_INFO`、`PX4_WARN`、`PX4_ERR`、`PX4_DEBUG`。 其中警告和错误会被额外添加到 [ULog](../log/ulog_file_format.md) 中，且还会在 [Flight Review](https://logs.px4.io/) 中显示。

1. 创建并打开一个名为 **CMakeLists.txt** 的新的 *cmake* 定义文件。 复制下面的文本：
    
    ```cmake
    ############################################################################
    #
    #   Copyright (c) 2015 PX4 Development Team. All rights reserved.
    #
    # Redistribution and use in source and binary forms, with or without
    # modification, are permitted provided that the following conditions
    # are met:
    #
    # 1. Redistributions of source code must retain the above copyright
    #    notice, this list of conditions and the following disclaimer.
    # 2. Redistributions in binary form must reproduce the above copyright
    #    notice, this list of conditions and the following disclaimer in
    #    the documentation and/or other materials provided with the
    #    distribution.
    # 3. Neither the name PX4 nor the names of its contributors may be
    #    used to endorse or promote products derived from this software
    #    without specific prior written permission.
    #
    # THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    # "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    # LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
    # FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
    # COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
    # INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
    # BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
    # OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
    # AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
    # LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
    # ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
    # POSSIBILITY OF SUCH DAMAGE.
    #
    ############################################################################
    px4_add_module(
    MODULE examples__px4_simple_app
    MAIN px4_simple_app
    STACK_MAIN 2000
    SRCS
        px4_simple_app.c
    DEPENDS
    )
    ```
    
    The `px4_add_module()` method builds a static library from a module description.
    
    * The `MODULE` block is the Firmware-unique name of the module (by convention the module name is prefixed by parent directories back to `src`).
    * The `MAIN` block lists the entry point of the module, which registers the command with NuttX so that it can be called from the PX4 shell or SITL console.
    
    > **Tip** The `px4_add_module()` format is documented in [PX4-Autopilot/cmake/px4_add_module.cmake](https://github.com/PX4/PX4-Autopilot/blob/{{ book.px4_version }}/cmake/px4_add_module.cmake).
    
    <span></span>
    
    > **Note** If you specify `DYNAMIC` as an option to `px4_add_module`, a *shared library* is created instead of a static library on POSIX platforms (these can be loaded without having to recompile PX4, and shared to others as binaries rather than source code). Your app will not become a builtin command, but ends up in a separate file called `examples__px4_simple_app.px4mod`. You can then run your command by loading the file at runtime using the `dyn` command: `dyn ./examples__px4_simple_app.px4mod`

## 编译应用程序/固件

应用程序的编写至此完成。 为了保证改程序可以被运行，你首先需要确保编译器会将它作为 PX4 固件的一部分进行编译。 应用程序将根据与你的硬件平台相对应的 *cmake* 文件被添加到 build/firmware 文件夹下。

* PX4 SITL (Simulator): [PX4-Autopilot/boards/px4/sitl/default.cmake](https://github.com/PX4/PX4-Autopilot/blob/master/boards/px4/sitl/default.cmake)
* Pixhawk v1/2: [PX4-Autopilot/boards/px4/fmu-v2/default.cmake](https://github.com/PX4/PX4-Autopilot/blob/master/boards/px4/fmu-v2/default.cmake)
* Pixracer (px4/fmu-v4): [PX4-Autopilot/boards/px4/fmu-v4/default.cmake](https://github.com/PX4/PX4-Autopilot/blob/master/boards/px4/fmu-v4/default.cmake)
* *cmake* files for other boards can be found in [PX4-Autopilot/boards/](https://github.com/PX4/PX4-Autopilot/tree/master/boards)

要启用将应用程序编译到固件中, 请在 *cmake* 文件中的某个位置为应用程序创建新行：

    examples/px4_simple_app
    

> **Note** 大多数 cmake 文件都已经添加好了这一行内容，因为固件中默认包含了所有的示例应用程序。

针对不同的平台使用相应的代码进行示例程序的编译：

* jMAVSim 仿真器：`make px4_sitl_default jmavsim`
* Pixhawk v1/2：`make px4_fmu-v2_default`（或只用 `make px4_fmu-v2`）
* Pixhawk v3：`make px4_fmu-v4_default`
* 其他飞控板：[构建代码](../setup/building_px4.md#building_nuttx)

## 测试应用（硬件）

### 将固件上传至飞控板

启用固件上传程序, 然后重置飞控板：

* Pixhawk v1/2：`make px4_fmu-v2_default upload`
* Pixhawk v3：`make px4_fmu-v4_default upload`

在你完成飞控板的重置之前应该会输出一些编译消息，并最终出现：

```sh
Loaded firmware for X,X, waiting for the bootloader...
```

一旦飞控板被重置并完成了固件的上传，命令行界面将输出：

```sh
Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

[100%] Built target upload
```

### 连接至控制台

现在，通过串口或者 USB 连接至 [PX4 系统控制台](../debug/system_console.md) 。 敲击 **ENTER** 键然后会出现控制台 shell 界面提示符：

```sh
nsh>
```

键入 "help" 并回车：

```sh
nsh> help
  help usage:  help [-v] [<cmd>]

  [           df          kill        mkfifo      ps          sleep       
  ?           echo        losetup     mkrd        pwd         test        
  cat         exec        ls          mh          rm          umount      
  cd          exit        mb          mount       rmdir       unset       
  cp          free        mkdir       mv          set         usleep      
  dd          help        mkfatfs     mw          sh          xd          

Builtin Apps:
  reboot
  perf
  top
  ..
  px4_simple_app
  ..
  sercon
  serdis
```

请注意，此时 `px4_simple_app` 已经是一个可用的命令了。 键入 `px4_simple_app` 并回车以运行该程序：

```sh
nsh> px4_simple_app
Hello Sky!
```

该应用程序现在已经被正确地注册到了 Px4 系统中，并且可以通过对其进行扩展来执行更有用的任务了。

## 测试应用（SITL）

如果你使用的是 SITL 仿真，那么 *PX4 控制台* 会默认启动（参见 [Building the Code > First Build (Using the jMAVSim Simulator)](../setup/building_px4.md#jmavsim_build) ）。 与 *nsh 控制台* (见上一节) 一样，您可以键入 `help` 以查看内置应用的列表。

输入 `px4_simple_app` 以运行该最小的应用程序。

```sh
pxh> px4_simple_app
INFO  [px4_simple_app] Hello Sky!
```

现在可以扩展应用程序以实际执行有用的任务。

## 订阅传感器数据

为了做一些更有用的事情，应用程序需要订阅一些输入量并发布输出指令（比如电机或者舵机指令）。

> **Tip** PX4 对硬件层进行抽象化的好处在这里发挥了作用！ 我们在构建应用程序时无需直接与传感器驱动进行任何的交互，且即便对飞控板或者传感器硬件进行更新后也不需要对你的应用程序进行任何更新。

各应用之间的消息通道被称为 [topics](../middleware/uorb.md) 。 For this tutorial, we are interested in the [sensor_combined](https://github.com/PX4/PX4-Autopilot/blob/master/msg/sensor_combined.msg) topic, which holds the synchronized sensor data of the complete system.

订阅一个 topic 非常简单直接：

```cpp
#include <uORB/topics/sensor_combined.h>
..
int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));
```

`sensor_sub_fd` 是一个 topic 句柄（handle），它可以高效地执行阻断以等待新数据。 待新数据抵达后调度程序会自动将当前进程从休眠中唤醒，线程在等待期间不会占用任何 CPU 周期。 为了实现这一功能，我们使用了 POSIX 系统调用函数 [poll()](http://pubs.opengroup.org/onlinepubs/007908799/xsh/poll.html) 。

将 `poll()` 加入消息订阅的实现过程如下 (*伪代码实现，完整的代码实现见下文*) ：

```cpp
#include <poll.h>
#include <uORB/topics/sensor_combined.h>
..
int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));

/* one could wait for multiple topics with this technique, just using one here */
px4_pollfd_struct_t fds[] = {
    { .fd = sensor_sub_fd,   .events = POLLIN },
};

while (true) {
    /* wait for sensor update of 1 file descriptor for 1000 ms (1 second) */
    int poll_ret = px4_poll(fds, 1, 1000);
    ..
    if (fds[0].revents & POLLIN) {
        /* obtained data for the first file descriptor */
        struct sensor_combined_s raw;
        /* copy sensors raw data into local buffer */
        orb_copy(ORB_ID(sensor_combined), sensor_sub_fd, &raw);
        PX4_INFO("Accelerometer:\t%8.4f\t%8.4f\t%8.4f",
                    (double)raw.accelerometer_m_s2[0],
                    (double)raw.accelerometer_m_s2[1],
                    (double)raw.accelerometer_m_s2[2]);
    }
}
```

使用下面的命令重新编译 app ：

```sh
make
```

### 测试 uORB 消息订阅

最后一步就是将你的应用程序作为后台进程/任务进行启动，在 nsh shell 界面输入：

```sh
px4_simple_app &
```

你的 app 会在控制台界面输出 5 组传感器数据然后退出：

```sh
[px4_simple_app] Accelerometer:   0.0483          0.0821          0.0332
[px4_simple_app] Accelerometer:   0.0486          0.0820          0.0336
[px4_simple_app] Accelerometer:   0.0487          0.0819          0.0327
[px4_simple_app] Accelerometer:   0.0482          0.0818          0.0323
[px4_simple_app] Accelerometer:   0.0482          0.0827          0.0331
[px4_simple_app] Accelerometer:   0.0489          0.0804          0.0328
```

> **Tip** 编写可使用命令行直接进行控制的后台进程请参阅： [Module Template for Full Applications](../apps/module_template.md) 。

## 发布数据

为了使用你的 app 计算好的输出量，接下来我们需要将这些结果 *发布* 出去。 接下来我们展示一下如何发布 attitude （姿态） topic 中的数据。

> **Note** 这里我们选取 `attitude` topic 是因为 *mavlink* app 会自动将该 topic 中的数据转发至地面控制站，这样可以方便我们查看这些结果。

数据的交互非常简单： 初始化想要发布的 topic 的 `结构体` 然后告诉这个 topic ：

```c
#include <uORB/topics/vehicle_attitude.h>
..
/* advertise attitude topic */
struct vehicle_attitude_s att;
memset(&att, 0, sizeof(att));
orb_advert_t att_pub_fd = orb_advertise(ORB_ID(vehicle_attitude), &att);
```

在主循环中完成了信息的处理之后就可以将其发布了：

```c
orb_publish(ORB_ID(vehicle_attitude), att_pub_fd, &att);
```

## 完整的示例代码

The [complete example code](https://github.com/PX4/PX4-Autopilot/blob/master/src/examples/px4_simple_app/px4_simple_app.c) is now:

```c
/****************************************************************************
 *

 *   Copyright (c) 2012-2019 PX4 Development Team. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 * 1. Redistributions of source code must retain the above copyright
 *    notice, this list of conditions and the following disclaimer.
 * 2. Redistributions in binary form must reproduce the above copyright
 *    notice, this list of conditions and the following disclaimer in
 *    the documentation and/or other materials provided with the
 *    distribution.
 * 3. Neither the name PX4 nor the names of its contributors may be
 *    used to endorse or promote products derived from this software
 *    without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
 * "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
 * LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
 * FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
 * COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
 * INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
 * BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
 * OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED
 * AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
 * LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
 * ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
 * POSSIBILITY OF SUCH DAMAGE.
 *
 ****************************************************************************/

/**
 * @file px4_simple_app.c
 * Minimal application example for PX4 autopilot
 *
 * @author Example User <mail@example.com>
 */

#include <px4_platform_common/px4_config.h>
#include <px4_platform_common/tasks.h>
#include <px4_platform_common/posix.h>
#include <unistd.h>
#include <stdio.h>
#include <poll.h>
#include <string.h>
#include <math.h>

#include <uORB/uORB.h>
#include <uORB/topics/sensor_combined.h>
#include <uORB/topics/vehicle_attitude.h>

__EXPORT int px4_simple_app_main(int argc, char *argv[]);

int px4_simple_app_main(int argc, char *argv[])
{
    PX4_INFO("Hello Sky!");

    /* subscribe to sensor_combined topic */
    int sensor_sub_fd = orb_subscribe(ORB_ID(sensor_combined));
    /* limit the update rate to 5 Hz */
    orb_set_interval(sensor_sub_fd, 200);

    /* advertise attitude topic */
    struct vehicle_attitude_s att;
    memset(&att, 0, sizeof(att));
    orb_advert_t att_pub = orb_advertise(ORB_ID(vehicle_attitude), &att);

    /* one could wait for multiple topics with this technique, just using one here */
    px4_pollfd_struct_t fds[] = {
        { .fd = sensor_sub_fd,   .events = POLLIN },
        /* there could be more file descriptors here, in the form like:
         * { .fd = other_sub_fd,   .events = POLLIN },
         */
    };

    int error_counter = 0;

    for (int i = 0; i < 5; i++) {
        /* wait for sensor update of 1 file descriptor for 1000 ms (1 second) */
        int poll_ret = px4_poll(fds, 1, 1000);

        /* handle the poll result */
        if (poll_ret == 0) {
            /* this means none of our providers is giving us data */
            PX4_ERR("Got no data within a second");

        } else if (poll_ret < 0) {
            /* this is seriously bad - should be an emergency */
            if (error_counter < 10 || error_counter % 50 == 0) {
                /* use a counter to prevent flooding (and slowing us down) */
                PX4_ERR("ERROR return value from poll(): %d", poll_ret);
            }

            error_counter++;

        } else {

            if (fds[0].revents & POLLIN) {
                /* obtained data for the first file descriptor */
                struct sensor_combined_s raw;
                /* copy sensors raw data into local buffer */
                orb_copy(ORB_ID(sensor_combined), sensor_sub_fd, &raw);
                PX4_INFO("Accelerometer:\t%8.4f\t%8.4f\t%8.4f",
                     (double)raw.accelerometer_m_s2[0],
                     (double)raw.accelerometer_m_s2[1],
                     (double)raw.accelerometer_m_s2[2]);

                /* set att and publish this information for other apps
                 the following does not have any meaning, it's just an example
                */
                att.q[0] = raw.accelerometer_m_s2[0];
                att.q[1] = raw.accelerometer_m_s2[1];
                att.q[2] = raw.accelerometer_m_s2[2];

                orb_publish(ORB_ID(vehicle_attitude), att_pub, &att);
            }

            /* there could be more file descriptors here, in the form like:
             * if (fds[1..n].revents & POLLIN) {}
             */
        }
    }

    PX4_INFO("exiting");

    return 0;
}
```

## 运行完整的示例

最后运行你的 app ：

```sh
px4_simple_app
```

If you start *QGroundControl*, you can check the sensor values in the real time plot ([Analyze > MAVLink Inspector](https://docs.qgroundcontrol.com/en/analyze_view/mavlink_inspector.html)).

## 总结

本教程介绍了开发一个基本的 PX4 自动驾驶仪应用程序需要涉及的一切内容。 Keep in mind that the full list of uORB messages/topics is [available here](https://github.com/PX4/PX4-Autopilot/tree/master/msg/) and that the headers are well documented and serve as reference.

更多信息和故障排除 /常见的陷阱等可以在这里找到： [uORB](../middleware/uorb.md)。

下一页提供了一个可用于编写具备启动和停止功能的完整应用程序的模版文件。