# Pulse - System Monitor

![Pulse Preview](./preview.png)

Real-time monitoring of CPU, RAM, disk, network, and temperatures in your terminal.

## Install

```bash
# Copy the script to your bin folder
cp pulse ~/.local/bin/
chmod +x ~/.local/bin/pulse

# Add to PATH if needed
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Test
pulse --version
```

Or system-wide:
```bash
sudo cp pulse /usr/local/bin/
sudo chmod +x /usr/local/bin/pulse
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

## License

MIT - See LICENSE.md
