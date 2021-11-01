!REDIRECT "https://docs.px4.io/master/zh/middleware/modules_template.html"

# 模块参考: 模板

## 模块

Source: [templates/template_module](https://github.com/PX4/Firmware/tree/master/src/templates/template_module)

### 描述

该部分描述所提供模块的功能。

这是一个模块的模版，该模块在后台作为任务（task）运行并且有 start/stop/status 功能。

### 实现

该部分描述模块的高层次实现。

### 示例

CLI 命令行用法示例：

    module start -f -p 42
    

<a id="module_usage"></a>

### Usage

    module &lt;command&gt; [arguments...]
     Commands:
       start
         [-f]        可选的示例标志
         [-p &lt;val&gt;]  可选的示例参数
                     默认值：0
    
       stop
    
       status        打印状态信息
    

## work_item_example

Source: [examples/work_item](https://github.com/PX4/Firmware/tree/master/src/examples/work_item)

### Description

Example of a simple module running out of a work queue.

<a id="work_item_example_usage"></a>

### Usage

    work_item_example <command> [arguments...]
     Commands:
       start
    
       stop
    
       status        print status info