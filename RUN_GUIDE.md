# 运行指南

## 环境准备

```bash
# 安装依赖（需 Python >= 3.12.9）
pip install -e . -i https://mirrors.aliyun.com/pypi/simple/

# 设置 matplotlib 后端（避免 PySide6 的 Qt 插件冲突）
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

可用控制器名称：
- `PurePursuit`
- `Stanley`
- `RearWheelFeedback`
- `LQRKinematic`
- `LQRDynamic`
- `MPC_XY_Frame`
- `MPC_Frenet_Frame`
