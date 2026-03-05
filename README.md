# ⚡ Pulse - System Monitor v1.1

Pulse is a professional, minimalist, high-performance system monitor for the terminal. Designed with a refined "Expert Mode" aesthetic, it provides a clear visualization of critical hardware metrics with minimal impact on system resources.

## 📸 Preview

![Preview](preview.png)

## ✨ Key Features
* **Real-Time Telemetry**: Dynamic monitoring of CPU load, frequency (MHz), RAM, storage, network, temperatures, and battery
* **Advanced Hardware Detection**: Accurate identification of GPU architectures and modern processors
* **Dynamic Graphics**: Visual CPU load history using block characters
* **Temperature Monitoring**: Real-time CPU and GPU temperature tracking
* **Battery Status**: Live battery level and charging status for laptops
* **Optimized Design**: Tailored for modern terminals, recommended for **Dark Blue** backgrounds
* **Cross-Platform**: Compatible with AMD, Intel, and NVIDIA hardware

## 🚀 Installation & Configuration

### Prerequisites
Pulse requires the following dependencies for full functionality:

```bash
sudo apt update && sudo apt install lm-sensors upower pciutils bc x11-utils -y
```
##Dependencies by Distro:
Debian/Ubuntu/Mint: sudo apt install bc pciutils mesa-utils
Fedora: sudo dnf install bc pciutils mesa-utils
Arch Linux: sudo pacman -S bc pciutils mesa-utils

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

# Monitor specific disk
DISK_PATH=/home pulse

# Monitor with custom window manager
WM="i3" pulse
```

### Environment Variables
- `DISK_PATH`: Specify disk partition to monitor (default: `/`)
- `WM`: Override window manager detection

## 🛠️ Technical Specifications

| Component | Technology |
|-----------|-------------|
| **Data Source** | `/proc/stat`, `/proc/net/dev`, `/sys/class/thermal/` |
| **Engine** | Pure Bash with ANSI escape sequences |
| **Architecture** | Optimized for minimal resource usage |
| **Refresh Rate** | 1 second intervals |
| **Compatibility** | Linux kernels 4.0+, systemd-based distributions |

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
Pulse is optimized for minimal impact. If experiencing lag:
- Ensure terminal supports ANSI escape sequences
- Check system load with `top`

## 🤝 Contributing

Contributions are welcome! Please ensure:
- Code follows existing style
- Functions are well-documented
- Compatibility is maintained

## ☕ Support

If you find Pulse useful, please consider supporting its development:

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/retrolcdclock)

---

**Created with ❤️ by Carlos Corral | Pulse Active | 2026**
