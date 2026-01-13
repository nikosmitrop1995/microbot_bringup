# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-01-13

### Added
- Initial release of microbot_bringup package
- Launch file `bringup.launch.py` for complete robot bringup
- `joy_node` integration for joystick input handling from USB game controllers
- `teleop_twist_joy_node` integration for converting joystick input to ROS2 geometry_msgs/Twist velocity commands
- `micro_ros_agent` integration for micro-ROS communication over WiFi (UDP port 8888)
- PlayStation 5 controller configuration file (`config/ps5.config.yaml`) with optimized control mappings:
  - Linear velocity control on left stick X-axis (axis 1)
  - Angular velocity control on left stick Y-axis (axis 0)
  - Enable button on L1 shoulder button (button 4) for safety
  - Turbo button on R1 shoulder button (button 5) for increased speed
- Configurable joystick deadzone (0.3) and autorepeat rate (20.0 Hz) for improved control responsiveness
- Launch arguments for runtime customization:
  - `joy_vel`: Velocity command topic name (default: `cmd_vel`)
  - `joy_config`: Controller configuration file name without extension (default: `ps5`)
  - `joy_dev`: Joystick device path (default: `/dev/input/js0`)
- Support for custom controller configurations via YAML files in `config/` directory
- Configurable linear and angular velocity scaling with turbo mode support
- Dynamic topic remapping for velocity commands via launch arguments
- ROS2 package structure with CMakeLists.txt and package.xml
- Comprehensive documentation in README.md with installation, configuration, usage examples, and troubleshooting
- CHANGELOG.md following Keep a Changelog format
- CMakeLists.txt configuration for installing launch files and configuration files

### Technical Details
- ROS2 distribution: Humble or later
- Dependencies: `joy`, `teleop_twist_joy`, `micro_ros_agent`, `geometry_msgs`
- Transport: WiFi (UDP)
- Micro-ROS agent port: 8888
- Default joystick device: `/dev/input/js0`
- Default velocity topic: `cmd_vel`
- Joystick deadzone: 0.3
- Autorepeat rate: 20.0 Hz
- PS5 controller linear scale: 0.7 (normal), 1.5 (turbo)
- PS5 controller angular scale: 0.4
