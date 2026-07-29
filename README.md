# Pulse - System Monitor v1.5

![Pulse Preview](./preview.png)

Real-time monitoring of CPU, RAM, disk, network, and temperatures in your terminal.

## Installation

To install Pulse v1.5, follow these steps:

### 1. Copy the script to your bin folder
```bash
cp pulse ~/.local/bin/
chmod +x ~/.local/bin/pulse
```

### 2. Copy the desktop file to applications folder
```bash
cp pulse.desktop ~/.local/share/applications/
```

### 3. Copy the icon to icons folder
```bash
cp pulse.svg ~/.local/share/icons/
```

### 4. Add to PATH if needed
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 5. Test installation
```bash
pulse --version
```

Or system-wide installation:
```bash
sudo cp pulse /usr/local/bin/
sudo chmod +x /usr/local/bin/pulse
sudo cp pulse.desktop /usr/share/applications/
sudo cp pulse.svg /usr/share/icons/
```

## Usage

```bash
pulse              # Start monitoring
pulse --quiet      # Single-line mode
pulse -i 2         # Refresh every 2 seconds
```

## Options

- `-h, --help` - Show help
- `-v, --version` - Show version  
- `-i, --interval N` - Refresh interval (seconds)
- `-q, --quiet` - Single-line output

## Environment

```bash
DISK_PATH=/home pulse    # Monitor /home instead of /
WM=i3 pulse              # Override window manager
```

## Requirements

- Bash 4.0+
- Linux system
- Optional: `lm-sensors` (temperatures), `nvidia-utils` (GPU), `upower` (battery)

## Troubleshooting

If Pulse doesn't display all information correctly, you may need to install optional dependencies:

### Temperature monitoring (lm-sensors)
**Debian/Ubuntu/Linux Mint:**
```bash
sudo apt update
sudo apt install lm-sensors
sudo sensors-detect
```

**Fedora/RHEL/CentOS:**
```bash
sudo dnf install lm_sensors
sudo sensors-detect
```

**Arch Linux:**
```bash
sudo pacman -S lm_sensors
sudo sensors-detect
```

### GPU monitoring
For NVIDIA GPUs, install the appropriate drivers:
**Debian/Ubuntu/Linux Mint:**
```bash
sudo apt install nvidia-utils
```

**Fedora/RHEL/CentOS:**
```bash
sudo dnf install nvidia-utils
```

**Arch Linux:**
```bash
sudo pacman -S nvidia-utils
```

For AMD/Intel GPUs, temperature monitoring is handled by lm-sensors (see above).

### Battery monitoring (upower)
**Debian/Ubuntu/Linux Mint:**
```bash
sudo apt install upower
```

**Fedora/RHEL/CentOS:**
```bash
sudo dnf install upower
```

**Arch Linux:**
```bash
sudo pacman -S upower
```

### GPU information (glxinfo)
**Debian/Ubuntu/Linux Mint:**
```bash
sudo apt install mesa-utils
```

**Fedora/RHEL/CentOS:**
```bash
sudo dnf install mesa-utils
```

**Arch Linux:**
```bash
sudo pacman -S mesa-utils
```

## License

MIT - See LICENSE.md

Support
https://ko-fi.com/retrolcdclock
