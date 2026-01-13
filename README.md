# microbot_bringup

A ROS 2 bringup package for microBot that launches joystick teleoperation and micro-ROS agent nodes. The package provides a complete launch configuration for controlling a robot via a PlayStation 5 controller, with velocity commands published to the robot through micro-ROS over WiFi.

## Installation

### Prerequisites

- ROS 2 (Humble or later)
- `joy` package: `sudo apt install ros-<distro>-joy`
- `teleop_twist_joy` package: `sudo apt install ros-<distro>-teleop-twist-joy`
- `micro_ros_agent` package: `sudo apt install ros-<distro>-micro-ros-agent`

### Building the Package

```bash
cd ~/ros2_ws/src
git clone git@github.com:nikosmitrop1995/microbot_bringup.git
cd ~/ros2_ws
colcon build --packages-select microbot_bringup
source install/setup.bash
```

## Configuration

The package includes a default PlayStation 5 controller configuration in `config/ps5.config.yaml`. You can customize the controller mapping by editing this file or creating a new configuration file.

### Default PS5 Configuration

- **Linear axis**: Left stick X-axis (axis 1)
- **Angular axis**: Left stick Y-axis (axis 0)
- **Enable button**: L1 shoulder button (button 4)
- **Turbo button**: R1 shoulder button (button 5)
- **Linear scale**: 0.7 (normal), 1.5 (turbo)
- **Angular scale**: 0.4

### Creating Custom Controller Configurations

1. Create a new YAML file in the `config/` directory (e.g., `xbox.config.yaml`)
2. Follow the same structure as `ps5.config.yaml`
3. Launch with your custom config: `ros2 launch microbot_bringup bringup.launch.py joy_config:=xbox`

## Usage

### Basic Launch

```bash
ros2 launch microbot_bringup bringup.launch.py
```

This launches:
- `joy_node`: Reads input from `/dev/input/js0`
- `teleop_twist_joy_node`: Converts joystick input to `cmd_vel` commands
- `micro_ros_agent`: Micro-ROS agent listening on UDP port 8888

### Launch Arguments

- `joy_vel`: Topic name for velocity commands (default: `cmd_vel`)
- `joy_config`: Controller configuration file name without extension (default: `ps5`)
- `joy_dev`: Joystick device path (default: `/dev/input/js0`)

### Examples

```bash
# Use a different controller configuration
ros2 launch microbot_bringup bringup.launch.py joy_config:=xbox

# Use a different joystick device
ros2 launch microbot_bringup bringup.launch.py joy_dev:=/dev/input/js1

# Publish to a different velocity topic
ros2 launch microbot_bringup bringup.launch.py joy_vel:=/robot/cmd_vel

# Combine multiple arguments
ros2 launch microbot_bringup bringup.launch.py \
    joy_config:=xbox \
    joy_dev:=/dev/input/js1 \
    joy_vel:=/robot/cmd_vel
```

## Troubleshooting

### Joystick Not Detected

- Verify the device exists: `ls -l /dev/input/js*`
- Check USB connection
- Verify permissions: add your user to the `input` group: `sudo usermod -a -G input $USER` (log out and back in)
- Test joystick input: `jstest /dev/input/js0`

### No Velocity Commands Published

- Verify `joy_node` is running: `ros2 node list | grep joy`
- Check joystick topic: `ros2 topic echo /joy`
- Verify controller configuration file exists in `config/` directory
- Check that the enable button is pressed (if configured)

### Micro-ROS Agent Connection Issues

- Verify the agent is running: `ros2 node list | grep micro_ros_agent`
- Check UDP port 8888 is not blocked by firewall
- Ensure the robot's firmware is configured with the correct agent IP address and port
- Verify network connectivity between the robot and the agent host
