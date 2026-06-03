# ⚡ Pulse - System Monitor v1.2

Pulse is a professional, minimalist, high-performance system monitor for the terminal. Designed with a refined "Expert Mode" aesthetic, it provides a clear visualization of critical hardware metrics with minimal impact on system resources.

## 📸 Preview

![Preview](preview.png)

## ✨ Key Features
* **Real-Time Telemetry**: Dynamic monitoring of CPU load, frequency (MHz), RAM, storage, network, temperatures, and battery
* **Advanced Hardware Detection**: Accurate identification of GPU architectures and modern processors
* **Dynamic Graphics**: Visual CPU load history using block characters
* **Temperature Monitoring**: Real-time CPU and GPU temperature tracking with caching for better performance
* **Battery Status**: Live battery level and charging status for laptops
* **Optimized Design**: Tailored for modern terminals, recommended for **Dark Blue** backgrounds
* **Cross-Platform**: Compatible with AMD, Intel, and NVIDIA hardware
* **Multi-Distro Support**: Works with Debian/Ubuntu, Fedora/openSUSE (RPM), and Arch Linux (pacman)
* **Wayland Support**: Full support for Wayland display servers
* **Command Line Options**: Customizable refresh interval and quiet mode
* **Error Handling**: Robust error handling with bash strict mode

## 🚀 Installation & Configuration

### Prerequisites
Pulse requires the following dependencies for full functionality:

```bash
sudo apt update && sudo apt install lm-sensors upower pciutils bc x11-utils -y
```

### Sensor Configuration
Configure temperature sensors for accurate readings:

```bash
# Auto-detect available sensors
sudo sensors-detect --auto

# Load detected sensor module (example: nct6775)
sudo modprobe nct6775
```

### Installation Steps

1. **Create local bin directory**
```bash
mkdir -p ~/.local/bin
```

2. **Install Pulse**
```bash
cp pulse ~/.local/bin/
chmod +x ~/.local/bin/pulse
```

3. **Update PATH**
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## 💻 Usage

### Basic Usage
```bash
# Run with default settings
pulse

# Show help
pulse --help

# Show version
pulse --version

# Set custom refresh interval (e.g., 2 seconds)
pulse --interval 2

# Quiet mode (minimal output)
pulse --quiet

# Monitor specific disk
DISK_PATH=/home pulse

# Monitor with custom window manager
WM="i3" pulse
```

### Environment Variables
- `DISK_PATH`: Specify disk partition to monitor (default: `/`)
- `WM`: Override window manager detection

### Command Line Options
- `-i, --interval SECONDS`: Set refresh interval in seconds (default: 1)
- `-q, --quiet`: Enable quiet mode with minimal output
- `-h, --help`: Show help message
- `-v, --version`: Show version information

## 🛠️ Technical Specifications

| Component | Technology |
|-----------|-------------|
| **Data Source** | `/proc/stat`, `/proc/net/dev`, `/sys/class/thermal/` |
| **Engine** | Pure Bash with ANSI escape sequences |
| **Architecture** | Optimized for minimal resource usage with caching |
| **Refresh Rate** | Configurable (default: 1 second intervals) |
| **Compatibility** | Linux kernels 4.0+, systemd-based distributions, Wayland & X11 |
| **Package Managers** | dpkg (Debian/Ubuntu), rpm (Fedora/openSUSE), pacman (Arch Linux) |

## 🔧 Troubleshooting

### Temperature Shows 0°C
```bash
# Reconfigure sensors
sudo sensors-detect --auto
sudo modprobe <detected_module>

# Verify sensor output
sensors
```

### No Battery Information
Desktop systems show "No Battery" - this is normal behavior.

### Performance Issues
Pulse is optimized for minimal impact with external command caching. If experiencing lag:
- Ensure terminal supports ANSI escape sequences
- Check system load with `top`
- Try increasing refresh interval: `pulse --interval 2`

### Wayland Support
Pulse automatically detects Wayland sessions. If you encounter display issues:
- Ensure you're running in a terminal emulator that supports Wayland
- The script will fall back to TTY mode if GUI detection fails

## 🤝 Contributing

Contributions are welcome! Please ensure:
- Code follows existing style
- Functions are well-documented
- Compatibility is maintained

## ☕ Support

If you find Pulse useful, please consider supporting its development:

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/retrolcdclock)

## 📋 Changelog

### v1.2 (Current)
- **Critical Bug Fix**: Fixed negative array index bug for bash < 4.3 compatibility
- **Error Handling**: Added `set -euo pipefail` for robust error handling
- **Cross-Distro Support**: Added support for RPM-based (Fedora, openSUSE) and Arch Linux (pacman)
- **Wayland Support**: Added automatic Wayland detection and support
- **Performance**: Implemented caching for external commands (sensors, nvidia-smi) to reduce overhead
- **Validation**: Added DISK_PATH validation to prevent errors
- **Code Quality**: Converted global variables to local in functions for better scoping
- **CLI Options**: Added command line arguments for interval, quiet mode, help, and version
- **Compatibility**: Improved compatibility with older bash versions

### v1.1
- Initial release with TTY and GUI mode support

---

**Created with ❤️ by Carlos Corral | Pulse Active | 2026**
