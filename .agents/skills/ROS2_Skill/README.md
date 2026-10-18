# ROS2 Skill (ROS_Programmer)

[![Skill Spec](https://img.shields.io/badge/AI--Skill-v2.0-orange.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![ROS 2](https://img.shields.io/badge/ROS-2%20(Humble%20%7C%20Iron%20%7C%20Jazzy%20%7C%20Rolling)-blue.svg)](#)

An AI agent skill for **ROS 2 engineering, workspace inspection, package development, debugging, simulation, navigation, control, URDF/TF2, sensors, rosbag workflows, and empirical ROS graph verification**.

---

## 📋 Features

- **ROS Environment Detection**: Detects ROS distribution, operating system, build system, and simulation environment without assumptions.
- **Strict Inspection & Interface Preservation**: Inspects `package.xml`, `CMakeLists.txt`, launch/config files, and prevents unintended interface breakages (topics, services, actions, QoS, TF).
- **Task Classification**: Categorizes tasks into packages, nodes, topics, actions, parameters, TF2, URDF/Xacro, ros2_control, Nav2, SLAM, sensors, QoS, simulation, and rosbag workflows.
- **Hardware Safety & Empirical Verification**: Enforces hardware safety rules and requires runtime empirical evidence before declaring task completion.

---

## 📁 Repository Structure

```
ROS_Programmer/
├── SKILL.md       # AI agent skill specification & ROS 2 engineering rules
├── README.md      # Documentation and usage guide
└── LICENSE        # MIT License
```

---

## 🚀 Usage & Integration

### With AI Coding Agents (Gemini, Claude, Antigravity CLI)
Place the `ROS_Programmer` directory into your agent's skills configuration folder:
```bash
~/.gemini/config/skills/ROS_Programmer/
```

When performing ROS 2 development, the agent will reference `SKILL.md` to guide environment inspection, debugging, and verification.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for details.
