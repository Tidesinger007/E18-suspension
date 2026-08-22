# Formula Student 悬架证据包中文总览

基于当前 `Suspension_Defense_Evidence` 文件夹生成。  
用途：车队内部交流、非悬架成员快速理解、Design Defense 准备。

本报告只汇总已经存在的 `.md`、`.csv`、PNG 和脚本结果，不重新计算，不编造 Adams 结果。

## 1. 先把证据边界说清楚

这份证据包里有三类内容，答辩时必须分开说：

| 证据类型 | 含义 | 目前能不能当最终仿真结果 |
| --- | --- | --- |
| 真实计算结果 | 由现有 CSV 和脚本得到的数值，例如 45% LLTD、1.8g 四轮载荷、弹簧参数研究 | 可以作为当前计算依据 |
| Pre-Adams 几何分析 | 使用第九版硬点做的二维前视几何检查 | 只能作为 Adams 前的趋势检查 |
| 尚未完成的 Adams 仿真 | Adams/Car 三维悬架模型、wheel travel、roll analysis、motion ratio 等 | 目前不能宣称完成 |

一句话概括：我们已经把轮胎数据、硬点和基础车辆动力学计算连起来了，但 Adams/Car 还没有完成，所以任何带 `Pre-Adams` 的图都不能说成 Adams 仿真结果。

## 2. 目前最重要的数字

| 项目 | 当前结果 | 解释 |
| --- | ---: | --- |
| 第九版硬点导出前轮距 | 1250 mm | 来自最终硬点轮心 y 坐标 |
| 第九版硬点导出后轮距 | 1230 mm | 与用户记录 1250 mm 不同 |
| 45% LLTD 前轴轮胎能力 | 2777 N | 由现有轮胎载荷敏感性模型得到 |
| 45% LLTD 后轴轮胎能力 | 4069 N | 后轴能力高于前轴 |
| 前/后能力比 | 0.683 | 表示前轴可用能力低于后轴 |
| 1.8g IF/OF/IR/OR 载荷 | 298 / 800 / 517 / 1131 N | 外侧后轮载荷最高 |
| Pre-Adams 前 camber gain | -0.0143 deg/mm | 二维几何检查 |
| Pre-Adams 后 camber gain | -0.0367 deg/mm | 二维几何检查 |
| 弹簧参数研究侧倾角范围 | 4.56 deg 到 2.28 deg | 简化 roll model，不是最终弹簧规格 |

## 3. 轮胎如何指导悬架

轮胎数据不是只用来选胎。它会告诉悬架组几件事：

- 轮胎在不同 FZ 下的抓地效率不同；
- 车身过弯时左右轮载荷会转移，所以 LLTD 会改变前后轴抓地能力；
- 轮胎对外倾角 Camber 敏感，所以悬架必须检查 wheel travel 和 body roll 后轮胎实际姿态；
- 弹簧和防倾杆不是只让车“不晃”，它们会通过 roll angle 影响动态 camber 和四轮载荷。

术语说明：

- `FZ`：单条轮胎受到的垂向载荷，单位 N。
- `LLTD`：Lateral Load Transfer Distribution，横向载荷转移分配，意思是过弯时前轴承担多少左右载荷差、后轴承担多少。
- `Camber`：从车头看轮胎向内或向外歪的角度。
- `Camber gain`：车轮上下跳动时外倾角变化的速度。
- `Pre-Adams`：Adams 前的简化几何检查，不是最终仿真。

## 4. 轮胎载荷敏感性

对应图：`07_Final_Figures/Figure_A_Tire_Load_Sensitivity.png`

这张图说明 Hoosier 43075 rim 7 在更高垂向载荷下，峰值 `|mu_y|` 有下降趋势。已有结果显示，峰值 `|mu_y|` 从约 `2.710` 下降到约 `2.432`。

通俗解释：外侧轮被压得更重后，虽然能产生更多绝对横向力，但“每 1 N 垂向载荷换来的抓地效率”会下降。因此左右轮载荷差越大，一对轮胎的总抓地效率通常越差。

这就是为什么要研究 LLTD。

## 5. 轮胎外倾敏感性

对应图：`07_Final_Figures/Figure_B_Tire_Camber_Sensitivity.png`

现有数据在 IA 0/2/4 deg 附近的峰值 `|mu_y|` 约为：

- IA 0 deg：2.488
- IA 2 deg：2.432
- IA 4 deg：2.397

注意：这里的 IA 是 TTC 试验里的 measured inclination angle，不要直接等同于赛车动态 camber 的正负号。

这张图的作用不是说“某一个 camber 一定最好”，而是说明轮胎确实对倾角敏感，所以悬架必须检查过弯时轮胎最终姿态。

## 6. 45% LLTD 检查

对应图：`07_Final_Figures/Figure_C_LLTD_vs_Axle_Capacity.png`

当前设计目标是：

- Front LLTD = 45%
- Rear LLTD = 55%

已有计算在 45% 前 LLTD 下得到：

- Front axle capacity：2777 N
- Rear axle capacity：4069 N
- Total capacity：6846 N
- Front/rear capacity ratio：0.683

在 35-55% 前 LLTD 扫描中，简单载荷模型给出的总四轮能力最高点约在 35% 前 LLTD，总能力约 6854 N。

结论口径：

45% LLTD 不能被说成“轮胎模型严格证明的唯一最优值”。更准确的说法是：45% 是当前 baseline，它可以用于讨论整车平衡和可调参数，但后续还要结合 Adams、实际弹簧/ARB、驾驶反馈和试车验证。

## 7. 1.8g 四轮载荷

对应图：`07_Final_Figures/Figure_H_1p8g_Four_Tire_Operating_States.png`

45% LLTD、1.8g 纯横向过弯下，当前计算得到：

| Tire | FZ (N) | Available lateral force (N) | 解释 |
| --- | ---: | ---: | --- |
| IF | 297.9 | 793.4 | 内侧前轮，卸载明显 |
| OF | 800.5 | 1983.8 | 外侧前轮，承担主要前轴横向力 |
| IR | 516.6 | 1318.5 | 内侧后轮，仍高于内侧前轮 |
| OR | 1130.9 | 2750.3 | 外侧后轮，四条里载荷最高 |

Figure H 同时画出了这些轮胎状态和 Pre-Adams 动态 camber 估计。它很适合内部交流，但必须说明：图中的 camber 坐标来自 1.5 deg roll reference 和 Pre-Adams camber 曲线，不是 Adams roll analysis。

## 8. 硬点检查

硬点就是悬架连接点的坐标，例如上下叉臂、推杆、减振器、转向拉杆和轮心。

目前使用的是：

- `E18_hardpoint_V6a (version 1).xlsx`
- 第九版（最终版）工作表
- 已导出到 `03_Adams_Model/E18_hardpoint_V6a_ninth_final_for_adams.csv`

重要发现：

- 第九版硬点导出的前轮距为 1250 mm；
- 第九版硬点导出的后轮距为 1230 mm；
- 这与用户记录的 1280/1250 mm 不一致；
- 当前报告明确按第九版硬点为准。

这不是偷偷修正，而是把差异写出来。

## 9. Pre-Adams Camber vs Wheel Travel

对应图：`07_Final_Figures/Figure_D_Camber_vs_Wheel_Travel_PreAdams.png`

`Wheel travel` 是车轮相对车身上下跳动的量，+ 表示 bump。

已有二维前视几何检查给出：

- Front camber gain near static：-0.0143 deg/mm
- Rear camber gain near static：-0.0367 deg/mm

通俗解释：车轮压缩时，悬架会让轮胎外倾角改变。这个变化是否有利，要和轮胎 camber sensitivity 一起看。

但这仍然不是 Adams 结果，因为它没有完整三维约束、toe、pushrod/rocker 和真实 motion ratio。

## 10. Pre-Adams Roll Center

对应图：`07_Final_Figures/Figure_E_Roll_Center_vs_Wheel_Travel_PreAdams.png`

Roll center 可以粗略理解为悬架几何支撑车身侧倾的高度。

Pre-Adams 静态估计：

- Front roll center height：9.0 mm
- Rear roll center height：47.1 mm

基于这个初算，45% LLTD 对应的弹性载荷转移目标大致为：

- Front elastic load difference：488.3 N
- Rear elastic load difference：500.8 N
- Elastic front roll stiffness share：49.4%

这些数字适合说明设计逻辑，但最终仍需 Adams 输出确认。

## 11. 弹簧参数研究

对应图：

- `07_Final_Figures/Figure_F_Wheel_Rate_vs_Roll_Angle.png`
- `07_Final_Figures/Figure_G_Wheel_Rate_vs_Dynamic_Camber.png`

弹簧参数研究不是寻找一个“唯一正确弹簧”。它的作用是给初始试车范围。

研究范围：

| Case | Front Hz | Rear Hz | Predicted roll angle (deg) | OF camber (deg) | OR camber (deg) |
| --- | ---: | ---: | ---: | ---: | ---: |
| Soft | 1.8 | 2.0 | 4.56 | 2.35 | 1.27 |
| Medium-soft | 2.0 | 2.2 | 3.75 | 1.66 | 0.77 |
| Medium | 2.2 | 2.4 | 3.13 | 1.14 | 0.40 |
| Medium-stiff | 2.4 | 2.6 | 2.65 | 0.74 | 0.11 |
| Stiff | 2.6 | 2.8 | 2.28 | 0.42 | -0.12 |

结论口径：

更高 wheel rate 会降低侧倾角，但这并不代表越硬越好。太硬可能让轮胎载荷波动变大。当前结果只能作为 `Parameter Study - not final vehicle hardware specification`。

## 12. Adams 和阻尼未完成项

当前 Adams 状态：

- Adams 2020 命令入口已找到；
- 但 `-help` 探测显示需要 Adams selection code；
- 本轮没有创建 verified Adams/Car 模型；
- 没有 Adams 导出的 camber、toe、roll center、motion ratio 或 body roll 结果。

下一步 Adams 必须完成：

1. 用第九版硬点建立前后 SLA suspension subsystem；
2. 跑 parallel wheel travel，建议 +/-30 mm；
3. 输出 camber vs wheel travel；
4. 输出 toe vs wheel travel；
5. 输出 roll center height vs wheel travel；
6. 输出 motion ratio vs wheel travel；
7. 跑 body roll analysis；
8. 用 Adams 动态 camber 替换当前 Pre-Adams 工况图。

阻尼状态：

- 找到 `TTX25-MkII-Dyno-N-vs-mmps.pdf`；
- 这是 Ohlins TTX25 MkII dyno 参考；
- 没有确认它是本车实测阻尼曲线；
- 因此不能宣称最终 damper setting。

## 13. 给各小组的阅读方式

| 小组 | 重点看什么 | 为什么 |
| --- | --- | --- |
| 悬架组 | 硬点、Pre-Adams 曲线、Adams 下一步 | 明确哪些结果能说，哪些不能说 |
| 电控组 | 1.8g 四轮载荷、前后轴能力 | 理解极限工况下四轮抓地力不是平均分配 |
| 气动组 | FZ 敏感性、外侧轮高载荷 | 理解平台和下压力会通过 FZ 影响轮胎能力 |
| 商业/答辩组 | 45% LLTD 口径、Adams 未完成边界 | 避免答辩时把 baseline 说成唯一最优 |

## 14. 最终建议

当前 PDF 可以用于内部统一语言和答辩准备。真正放进最终 Design Defense PPT 前，建议：

- 保留 Figure A/B/C 作为轮胎与 LLTD 依据；
- 保留 1.8g 四轮载荷表作为计算依据；
- 将 Figure D/E/H 中涉及 Pre-Adams 的部分替换为 Adams/Car 真实导出曲线；
- 明确说明 45% LLTD 是当前设计目标和 baseline，不是唯一最优；
- 阻尼部分只说参数研究和试车方向，不说最终设置。

