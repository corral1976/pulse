# Pulse - System Monitor v1.0.0

A minimalist and elegant system monitor for the terminal, designed for advanced GNU/Linux users. It offers real-time visualization of CPU (including frequency and history graphs), RAM, disk, network, and temperatures, featuring a design optimized for terminals with modern fonts.

## Features

- **Dual-mode display**: GUI with colors and TTY with ASCII
- **Real-time monitoring**: CPU, RAM, disk, network, and temperature metrics
- **Intelligent caching**: Performance optimization for sensor data
- **Quiet mode**: Single-line output for scripting and dashboards
- **Desktop integration**: System launcher and icon
- **Hardware support**: lm-sensors, NVIDIA/AMD GPU, battery monitoring

## Installation

### Debian/Ubuntu (.deb package)

```bash
sudo dpkg -i pulse-monitor_1.0.0_all.deb
```

### Build from source

```bash
# Clone repository
git clone https://gitlab.com/corral1976/pulse.git
cd pulse

# Build package
bash BUILD_DEB.sh

# Install
sudo dpkg -i pulse-monitor_1.0.0_all.deb
```

## Usage

```bash
pulse              # Start monitoring
pulse --quiet      # Single-line mode
pulse -i 2         # Refresh every 2 seconds
pulse --help       # Show help
pulse --version    # Show version
```

## Options

- `-h, --help` - Show help message
- `-v, --version` - Show version information
- `-i, --interval N` - Refresh interval in seconds (default: 1)
- `-q, --quiet` - Single-line minimal output
- `-n, --no-color` - Disable colored output

## Environment Variables

```bash
DISK_PATH=/home pulse    # Monitor /home instead of /
WM=i3 pulse              # Override window manager detection
```

## Requirements

- **Required**: Bash 4.0+, Linux system with /proc
- **Recommended** for enhanced functionality:
  - `lm-sensors` (CPU/GPU temperature)
  - `nvidia-utils` (NVIDIA GPU temperature)
  - `mesa-utils` (GPU information)
  - `pciutils` (GPU fallback)
  - `upower` (battery monitoring)
  - `x11-utils` (screen resolution)
  - `procps` (system utilities)

## Optional Dependencies Installation

### Debian/Ubuntu/Linux Mint
```bash
sudo apt install lm-sensors mesa-utils pciutils upower x11-utils procps
sudo sensors-detect
```

### Fedora/RHEL/CentOS
```bash
sudo dnf install lm_sensors mesa-utils pciutils upower x11-utils procps
sudo sensors-detect
```

### Arch Linux
```bash
sudo pacman -S lm_sensors mesa-utils pciutils upower x11-utils procps
sudo sensors-detect
```

## Removal

```bash
sudo dpkg -r pulse-monitor
```

## License

MIT License - See LICENSE file for details.

## Support

- **Repository**: https://gitlab.com/corral1976/pulse
- **Issues**: https://gitlab.com/corral1976/pulse/-/issues
- **Support**: https://ko-fi.com/retrolcdclock

## Author

Carlos Corral - Pulse Active
