!REDIRECT "https://docs.px4.io/master/bg/middleware/modules_driver_optical_flow.html"

# Modules Reference: Optical Flow (Driver)
## thoneflow
Source: [drivers/optical_flow/thoneflow](https://github.com/PX4/Firmware/tree/master/src/drivers/optical_flow/thoneflow)


### Description

Serial bus driver for the ThoneFlow-3901U optical flow sensor.

Most boards are configured to enable/start the driver on a specified UART using the SENS_TFLOW_CFG parameter.

Setup/usage information: https://docs.px4.io/en/sensor/thoneflow.html

### Examples

Attempt to start driver on a specified serial device.
```
thoneflow start -d /dev/ttyS1
```
Stop driver
```
thoneflow stop
```

<a id="thoneflow_usage"></a>

### Usage
```
thoneflow <command> [arguments...]
 Commands:
   start         Start driver
     -d <val>    Serial device

   stop          Stop driver

   info          Print driver information
```