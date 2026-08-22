# Suspension Defense Overview

这是一份给非悬架专业成员看的中文总结。它只汇总 `Suspension_Defense_Evidence` 中已经存在的 Markdown、CSV、PNG 和脚本输出，不重新计算，也不把 Pre-Adams 几何检查说成 Adams 仿真。

## 三类证据边界

- 真实计算结果：轮胎载荷敏感性、45% LLTD 下四轮 FZ、LLTD 扫描、弹簧参数研究。
- Pre-Adams 几何分析：用第九版硬点做的二维前视几何检查，包括 camber gain 和 roll center 初算。
- 尚未完成的 Adams 仿真：Adams 2020 命令入口存在，但没有完成可验证的 Adams/Car 模型和导出结果。

## 最重要数字

- 第九版硬点导出轮距：前 1250 mm，后 1230 mm。
- 45% Front LLTD：前轴轮胎能力 2777 N，后轴轮胎能力 4069 N。
- 1.8g 四轮载荷：IF 298 N / OF 800 N / IR 517 N / OR 1131 N。
- Pre-Adams camber gain：前 -0.0143 deg/mm，后 -0.0367 deg/mm。
- 弹簧参数研究：1.8g 预测侧倾角约 4.56 deg 到 2.28 deg。

## 图表清单

1. Figure A - Tire load sensitivity
2. Figure B - Tire camber sensitivity
3. Figure C - Front LLTD vs axle lateral capacity
4. Figure H - 1.8g four tire operating states
5. Figure D - Camber vs wheel travel, Pre-Adams
6. Figure E - Roll center height vs wheel travel, Pre-Adams
7. Figure F - Wheel rate vs roll angle
8. Figure G - Wheel rate vs dynamic camber

## 结论口径

45% LLTD 是当前设计目标，不是本轮计算证明出来的唯一最优值。当前证据说明它可以作为答辩中的 baseline 来讨论，但需要 Adams/Car 完成 camber、toe、roll center、motion ratio 和 body roll 结果后，才能把“悬架实际让轮胎处在合理区域”这句话说完整。

## 数据来源

- `08_Report/Suspension_Evidence_Report.md`
- `Suspension_Defense_Summary.md`
- `01_Tire/*.csv`
- `02_LLTD/*.csv`
- `03_Adams_Model/Adams_Model_Status.md`
- `04_Kinematics/*.csv`
- `05_1p8g_Corner/*.csv`
- `06_Spring_Damper/*.csv`
- `07_Final_Figures/*.png`
- `scripts/build_suspension_evidence.m`
