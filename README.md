# ⚡ Pulse - System Monitor v1.0

Pulse is a professional, minimalist, high-performance system monitor for the terminal. Designed with a refined "Expert Mode" aesthetic, it provides a clear visualization of critical hardware metrics with minimal impact on system resources.

## 📸 Vista previa

![Preview](preview.png)

## ✨ Key Features
* **Real-Time Telemetry**: Dynamic monitoring of CPU load, frequency (MHz), RAM, storage, and network.
* **Advanced Hardware Detection**: Accurate identification of GPU architectures and modern processors.
* **Dynamic Graphics**: Visual CPU load history using block characters.
* **Optimized Design**: Tailored for modern terminals, recommended for **Dark Blue** backgrounds.

## 🚀 Installation & Configuration

For professional integration, install Pulse in your local binary directory.

1. System Requirements
Install necessary dependencies:

sudo apt update && sudo apt install lm-sensors upower pciutils bc x11-utils -y

# Configure temperature sensors
sudo sensors-detect --auto
sudo modprobe nct6775  # Load detected sensor module

2. System Deployment

Follow these steps to install the binary correctly:
Bash

# Create local bin folder
mkdir -p ~/.local/bin

# Copy the script
cp pulse ~/.local/bin/

# Grant permissions
chmod +x ~/.local/bin/pulse

3. PATH Configuration

Add this line to the end of your ~/.bashrc to run it from anywhere:
Bash

export PATH="$HOME/.local/bin:$PATH"

Apply changes with: source ~/.bashrc
🛠️ Technical Specifications

    Data Source: Efficient extraction from /proc/stat and /proc/net/dev.

    Engine: Pure Bash and ANSI escape sequences.

    Architecture: Clean code optimized for advanced users.

☕ Support the Project

If you find Pulse useful, please consider supporting its development:

👉 Buy Me A Coffee

Direct Link: https://ko-fi.com/retrolcdclock

Created with ❤️ by Carlos Corral | Pulse Active | 2026
