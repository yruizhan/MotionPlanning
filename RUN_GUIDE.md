# 运行指南

## 项目简介

MotionPlanning 是一个自动驾驶运动规划与控制工具包（PyAuto），包含：

- **规划器**：Hybrid A*、State Lattice
- **控制器**：Pure Pursuit、Stanley、后轮反馈、LQR（运动学/动力学）、MPC（XY/Frenet）

## 前置条件

- **操作系统**：Linux / macOS / Windows
- **Python**：>= 3.12
- **系统依赖**：`tkinter`（用于 matplotlib 的 TkAgg 后端）
  ```bash
  # Ubuntu/Debian
  sudo apt install python3-tk
  # macOS (Homebrew Python 自带)
  # Windows (Python 安装包默认包含)
  ```

## 环境准备

```bash
# 安装依赖（国内用户使用阿里云镜像）
pip install -e . -i https://mirrors.aliyun.com/pypi/simple/

# 安装依赖（其他地区）
pip install -e .

# （可选）如果遇到 PySide6 的 Qt 插件冲突，设置 matplotlib 后端
export MPLBACKEND=TkAgg
```

---

## 规划器

```bash
# Hybrid A* 规划器
python3 -m pyauto.planning.HybridAstarPlanner.hybrid_astar

# Lattice 规划器
python3 -m pyauto.planning.LatticePlanner.lattice_planner
```

---

## 控制器仿真

以下命令均在项目根目录执行（无需 `cd tutorials`）：

```bash
# Pure Pursuit
python3 tutorials/simulation_runner_purepursuit.py

# Stanley
python3 tutorials/simulation_runner_stanley.py

# 后轮反馈 (Rear-Wheel Feedback)
python3 tutorials/simulation_runner_rear_wheel_feedback.py

# LQR 运动学模型
python3 tutorials/simulation_runner_LQR_Kinematic_Model.py

# LQR 动力学模型
python3 tutorials/simulation_runner_LQR_Dynamic_Model.py

# MPC (XY 坐标系)
python3 tutorials/simulation_runner_MPC_XY_Frame.py

# MPC (Frenet 坐标系)
python3 tutorials/simulation_runner_MPC_Frenet_Frame.py
```

### 通用运行器（支持多控制器对比）

```bash
# 单个控制器
python3 tutorials/generic_simulator.py --controller PurePursuit

# 多个控制器对比
python3 tutorials/generic_simulator.py --controller PurePursuit Stanley LQRDynamic

# 自定义参数
python3 tutorials/generic_simulator.py --controller PurePursuit --max_speed 15 --dt 0.05 --max_time 20
```

**可用参数：**

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--controller` | 控制器名称（必填，可多个） | — |
| `--max_speed` | 最大速度 (m/s) | 配置文件默认值 |
| `--dt` | 时间步长 (s) | 配置文件默认值 |
| `--max_time` | 每段最大仿真时间 (s) | 10.0 |

**可用控制器名称：**
- `PurePursuit`
- `Stanley`
- `RearWheelFeedback`
- `LQRKinematic`
- `LQRDynamic`
- `MPC_XY_Frame`
- `MPC_Frenet_Frame`
