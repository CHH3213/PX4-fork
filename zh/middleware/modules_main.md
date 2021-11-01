!REDIRECT "https://docs.px4.io/master/zh/middleware/modules_main.html"

# 模块 & 命令 参考

后续页面对 PX4 的模块、驱动和命令相关内容的进行了记录。 主要描述了各自提供的功能、功能实现的高层次总览以及如何使用命令行进行交互。

> **Note** **此列表是由源代码自动生成的** 并且包含了最新的模块文档。

它并不是一个完整的列表，NuttX 也会提供一些额外的命令（比如 `free`）。 在控制台使用 `help` 获取所有的可用命令，大部分情况下使用 `command help` 可以在控制台上打印出该命令的使用方法。

Since this is generated from source, errors must be reported/fixed in the [PX4-Autopilot](https://github.com/PX4/PX4-Autopilot) repository. 文档页可以在固件目录的根目录下运行如下命令生成：

    make module_documentation
    

生成的文件将被写入 `modules` 目录。

## 分类

- [命令](modules_command.md)
- [通信](modules_communication.md)
- [控制器](modules_controller.md)
- [驱动](modules_driver.md)
- [估计器](modules_estimator.md)
- [仿真](modules_simulation.md)
- [系统](modules_system.md)
- [模板](modules_template.md)