---
name: ROS2_Skill
description: ROS 2 engineering skill for workspace inspection, package development, debugging, simulation, navigation, control, URDF, TF2, sensors, rosbag workflows, and empirical ROS graph verification.
---

# ROS2 Skill

ROS2_Skill provides domain-specific engineering rules for working with ROS 2 workspaces.

It supplements the general Essential_Skill workflow. Essential_Skill controls planning, approval, execution orchestration, verification policy, and Git operations. ROS2_Skill controls ROS-specific analysis and implementation.

---

## 1. Core Rules

### Rule 1 — Detect ROS Environment

Never assume the ROS distribution.

Before ROS-specific work, inspect:

```bash
printenv ROS_DISTRO
```

Also determine:

* Operating system
* Workspace root
* ROS distribution
* Build system
* Package type
* Primary implementation language
* Simulation environment if present

Do not introduce APIs incompatible with the detected ROS distribution.

---

### Rule 2 — Inspect Before Modification

Before modifying a ROS workspace, inspect relevant:

* package.xml
* CMakeLists.txt
* setup.py
* setup.cfg
* source files
* launch files
* YAML configuration
* URDF/Xacro
* controller configuration
* existing topic/service/action names

Use:

```bash
colcon list
```

where available to understand workspace packages.

Do not modify unrelated packages.

---

### Rule 3 — Preserve ROS Interfaces

Do not silently change:

* Topic names
* Service names
* Action names
* Message types
* Frame IDs
* Parameter names
* QoS profiles
* Namespace structure

If an interface change is necessary, explicitly include it in the plan.

---

### Rule 4 — Prefer Existing ROS Standards

Use existing ROS 2 packages and standard interfaces where appropriate.

Prefer:

* geometry_msgs
* sensor_msgs
* nav_msgs
* std_msgs
* std_srvs
* builtin_interfaces

Do not create custom interfaces unless the required data cannot be represented cleanly using existing interfaces.

---

## 2. Task Classification

Classify ROS tasks into one or more categories:

* PACKAGE
* NODE
* TOPIC
* SERVICE
* ACTION
* PARAMETER
* TF2
* URDF_XACRO
* ROS2_CONTROL
* NAV2
* SLAM
* SENSOR
* SIMULATION
* ROSBAG
* QOS
* DEBUGGING

Load only the references relevant to the active task.

---

## 3. Workspace Inspection

Determine workspace structure before implementation.

Inspect for:

```text
src/
launch/
config/
urdf/
meshes/
worlds/
include/
test/
```

Identify package build types:

```text
ament_cmake
ament_python
```

Inspect package dependencies before adding new ones.

---

## 4. ROS Graph Inspection

When a ROS system is running, inspect the graph using appropriate commands:

```bash
ros2 node list
ros2 topic list
ros2 service list
ros2 action list
```

Use targeted inspection:

```bash
ros2 node info <node>
ros2 topic info <topic>
ros2 interface show <interface>
```

Do not infer message structure when it can be inspected directly.

---

## 5. Topic Debugging

For topic-related problems inspect:

```bash
ros2 topic list
ros2 topic info <topic>
ros2 topic echo <topic>
ros2 topic hz <topic>
ros2 topic bw <topic>
```

Check:

1. Topic exists
2. Correct message type
3. Publisher exists
4. Subscriber exists
5. QoS compatibility
6. Expected publication frequency
7. Data values are valid

---

## 6. QoS

Treat QoS as part of the ROS interface.

Inspect and reason about:

* Reliability
* Durability
* History
* Depth
* Deadline
* Lifespan

Sensor streams should not automatically use the same QoS settings as command/control channels.

Do not change QoS merely to make communication appear to work without identifying the actual incompatibility.

---

## 7. TF2

Before changing transforms inspect the existing TF tree.

Validate:

* Parent frame
* Child frame
* Frame naming
* Transform direction
* Timestamp
* Static vs dynamic transform

Use targeted validation such as:

```bash
ros2 run tf2_ros tf2_echo <parent> <child>
```

Avoid publishing duplicate transforms between the same frames.

---

## 8. URDF and Xacro

When modifying robot descriptions:

* Preserve existing frame hierarchy unless change is required
* Keep dimensions and units explicit
* Use SI units
* Avoid duplicated link names
* Avoid duplicated joint names
* Validate parent-child relationships
* Preserve mesh paths
* Do not modify physical geometry without requirement

For Xacro, prefer reusable properties and macros only when repetition justifies them.

Do not over-abstract simple robot descriptions.

---

## 9. ros2_control

Before modifying controllers identify:

* Hardware interface
* Joint interfaces
* Controller manager
* Controller type
* Update rate
* Command interfaces
* State interfaces

Do not issue hardware commands during validation without explicit approval.

Prefer simulation or inactive controller validation when possible.

---

## 10. Navigation and SLAM

For Nav2/SLAM tasks inspect:

* map
* odometry
* TF tree
* laser/depth topic
* robot footprint
* controller parameters
* planner parameters
* localization source

Do not begin parameter tuning until sensor data, transforms, and odometry are verified.

Debug in this order:

```text
Sensors
→ TF
→ Odometry
→ Localization
→ Planning
→ Control
```

---

## 11. Sensors

Before writing a new sensor node check whether an official or maintained ROS driver already exists.

Validate sensor data using:

* publication rate
* timestamp behavior
* frame_id
* units
* covariance where relevant
* physical plausibility

Do not treat malformed sensor data as a navigation problem.

---

## 12. Build Workflow

Prefer scoped builds:

```bash
colcon build --packages-select <package>
```

Use dependency builds where required:

```bash
colcon build --packages-up-to <package>
```

Do not automatically delete:

```text
build/
install/
log/
```

unless stale build artifacts are confirmed as the problem.

After building, source the correct workspace:

```bash
source install/setup.bash
```

Use the OS-appropriate equivalent when required.

---

## 13. Debugging Order

When a ROS application fails, investigate in this order:

```text
1. Environment
2. Package discovery
3. Build errors
4. Launch errors
5. Node state
6. ROS graph
7. Interface compatibility
8. QoS
9. TF
10. Parameters
11. Sensor data
12. Algorithm behavior
13. Hardware
```

Do not jump directly into algorithm rewrites.

---

## 14. Runtime Verification

A successful compilation is not sufficient verification.

Where applicable verify:

```bash
ros2 node list
ros2 node info <node>
ros2 topic list
ros2 topic info <topic>
ros2 topic echo <topic> --once
ros2 topic hz <topic>
```

For services:

```bash
ros2 service list
ros2 service type <service>
```

For actions:

```bash
ros2 action list
ros2 action info <action>
```

For parameters:

```bash
ros2 param list
ros2 param get <node> <parameter>
```

For lifecycle nodes:

```bash
ros2 lifecycle get <node>
```

Report evidence from validation before declaring success.

---

## 15. Hardware Safety

When connected to physical hardware:

* Never command motors automatically
* Never enable actuators automatically
* Never modify maximum velocity or acceleration limits silently
* Never bypass emergency-stop logic
* Never disable safety interlocks
* Never alter hardware limits without explicit authorization

Prefer simulation, dry-run, visualization, or inactive-controller tests first.

---

## 16. Completion Report

At completion provide:

```text
Goal
Files changed
ROS packages affected
Interfaces affected
Build result
Runtime verification
Remaining warnings
```

Do not claim success without empirical evidence where runtime validation is available.
