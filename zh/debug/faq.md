!REDIRECT "https://docs.px4.io/master/zh/debug/faq.html"

# 常见问题

## 编译错误

### 闪存溢出

> **Tip** 使用 FMUv4 架构获得双倍亮度。 The first available board from this generation is the [Pixracer](https://docs.px4.io/master/en/flight_controller/pixracer.html).

可以加载到主板上的代码量受到其具有的闪存量的限制。 当添加其他模块或代码时，添加可能会超过闪存。 这将导致 "闪存溢出"。 上游版本将始终生成，但取决于开发人员添加的内容，它可能会在本地溢出。

```sh
region `flash' overflowed by 12456 bytes
```

若要解决此问题，请使用较新的硬件或从生成中删除对您的用例不重要的模块。 The configuration is stored in **/PX4-Autopilot/boards/px4** (e.g. [PX4-Autopilot/boards/px4/fmu-v5/default.cmake](https://github.com/PX4/PX4-Autopilot/blob/master/boards/px4/fmu-v5/default.cmake)). 要删除模块，只需将其注释掉：

```cmake
#tune_control
```

## USB 错误

### 上传从不成功

在 Ubuntu 上，卸载modem manager：

```sh
sudo apt-get remove modemmanager
```