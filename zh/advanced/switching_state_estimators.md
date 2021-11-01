!REDIRECT "https://docs.px4.io/master/zh/advanced/switching_state_estimators.html"

# 更换状态估计器

此页显示了可用的状态估计器以及如何在它们之间切换。

> **Tip** 强烈推荐用于各种目的都使用 EKF2（LPE 已不再支持/维护）。

## 可用的估计器

可用的估计器如下：

- **EKF2 姿态、位置和风的状态估计器** - EKF2 是一个扩展卡尔曼过滤器，用于估计姿态、3D位置/速度和风状态。
- **LPE 位置估计器** - LPE位置估计器是一种扩展卡尔曼滤波器，用于 3D 位置和速度状态。
- **Q 姿态估计器** - 姿态Q估计器是一个非常简单、基于四元数的互补滤波器。

## 如何启用不同的估计器

对于多旋翼和 VTOL ，使用参数 [SYS_MC_EST_GROUP](../advanced/parameter_reference.md#SYS_MC_EST_GROUP) 来选择下面的配置（ LPE 不再支持固定翼飞机）。

| SYS_MC_EST_GROUP | Q Estimator | LPE | EKF2 |
| ------------------ | ----------- | --- | ---- |
| 1                  | 启用          | 启用  |      |
| 2                  |             |     | 启用   |
| 3                  | 启用          |     |      |

> **Note** 对于 FMU-v2 （只有它）你需要编译 PX4时指定使用哪个需要的估计器（例如使用 EKF2： `make px4_fmu-v2`，使用 LPE: `make px4_fmu-v2_lpe`）。 这是因为 FMU-v2 不具有足够的资源同时包含这两个估计器。 其他的 Pixhawk FMU 版本同时拥有两个估计器。