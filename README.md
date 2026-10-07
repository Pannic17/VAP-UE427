# V_UE427

VC-V 项目的主仓库，基于 **Unreal Engine 4.27**。工程包含视觉检测点处理的 C++ 代码、蓝图与场景资源，用于探索检测点驱动的星球、引力与粒子视觉效果。

## 相关仓库入口

| 仓库 | 定位 | 入口 |
| --- | --- | --- |
| **V_UE427（主仓库）** | Unreal Engine 场景、视觉表现与检测点处理 | [查看主仓库](https://github.com/Pannic17/V_UE427) |
| VAP-OpenCV-Detection | Python / OpenCV 摄像头预览及 Haar 级联检测实验 | [进入检测仓库](https://github.com/Pannic17/VAP-OpenCV-Detection) |
| VAP-Unity | Unity 摄像头处理、检测工具及星球交互原型 | [进入 Unity 仓库](https://github.com/Pannic17/VAP-Unity) |

三个仓库独立维护。上述链接用于导航；当前代码没有提供连接三者的统一通信协议或一键启动流程。

## 工程结构

```text
V_UE427.uproject             UE 工程入口，EngineAssociation 为 4.27
V_UE427.sln                  已有 Visual Studio 解决方案
Source/
  V_UE427/                  主 C++ 模块
    Public/CVProcessor.h    蓝图可调用的检测点处理接口
    Private/CVProcessor.cpp 坐标变换、距离筛选及引力计算
Content/                    场景、蓝图、模型、材质和视觉效果资源
Build/                      已跟踪的构建辅助文件
```

`ACVProcessor` 继承 `AHikVisionActor`，提供检测点数组构造、摄像头坐标映射、相对位置与引力方向计算等接口。主模块还依赖 `Niagara`。

已跟踪的场景包括 `Content/Detection.umap`、`Content/Planet.umap`、`Content/Final.umap`、`Content/Final1.umap` 和 `Content/Final2.umap`，可在编辑器中手动打开检查。

## 打开工程

1. 准备 Unreal Engine 4.27 和与该版本兼容的 Windows C++ 编译工具链。
2. 补齐提供 `HiKVision` 模块及 `HiKVisionActor.h` 的插件或 SDK。工程声明了该模块依赖，但仓库没有提供对应实现。
3. 确认工程中启用的 `GLTFImporter` 插件可用。
4. 对 `V_UE427.uproject` 生成 Visual Studio 项目文件，编译 `V_UE427Editor`，再打开工程。
5. 在编辑器中打开需要查看的地图，检查蓝图、插件和资源引用后进行运行测试。

## 当前状态与限制

- `.gitignore` 排除了 `Plugins/` 和 `Config/`，此次拉取也未包含这些目录的受跟踪文件。首次运行需恢复原项目所需的插件和配置。
- `CVProcessor.cpp` 中的 `IterateAllPlanet()` 仍为 TODO，不能视为已完成的星球更新流程。
- 摄像头坐标转换中使用固定的 `1920` 和 `1082` 尺寸，接入其他分辨率时需要核对映射参数。
- 本说明基于仓库源码与配置整理；尚未进行 UE 编译、插件接入或摄像头运行验证。
