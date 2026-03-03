# ⚡ Pulse - System Monitor v1.0

Pulse is a professional, minimalist, high-performance system monitor for the terminal. Designed with a refined "Expert Mode" aesthetic, it provides a clear visualization of critical hardware metrics with minimal impact on system resources.

## ✨ Key Features
- **Real-Time Telemetry**: Dynamic monitoring of CPU load, current frequency (MHz), RAM usage, storage status, and network traffic.
- **Advanced Hardware Detection**: Enhanced logic for accurate identification of various GPU architectures (integrated and dedicated) and modern processors.
- **Dynamic Graphics**: Visual CPU load history integrated directly into the interface using block characters.
- **Optimized Design**: Interface tailored for modern terminals, recommended for **Dark Blue** backgrounds.

## 🚀 Installation & Configuration

For a professional integration on GNU/Linux systems, it is recommended to install Pulse in the user's local binary directory to make it accessible globally.

### 1. System Requirements
Ensure you have the necessary dependencies installed for hardware detection and precision calculations:
```bash
sudo apt update && sudo apt install pciutils bc x11-utils -y

2. System Deployment

Follow these steps to install the binary into your local folder correctly:
Bash

# Create the local bin directory if it doesn't exist
mkdir -p ~/.local/bin

# Copy the script to the binary folder
# (Run this command from the directory where you downloaded the file)
cp pulse ~/.local/bin/

# Grant execution permissions to the binary
chmod +x ~/.local/bin/pulse

3. PATH Configuration

To run pulse by simply typing its name from any location, add the following line to the end of your ~/.bashrc file:
Bash

export PATH="$HOME/.local/bin:$PATH"

After saving, restart your terminal or apply the changes with source ~/.bashrc.
🛠️ Technical Specifications

    Data Source: Efficient metric extraction directly from /proc/stat and /proc/net/dev.

    Rendering Engine: Developed entirely in Bash using ANSI escape sequences for maximum compatibility and speed.

    Architecture: Clean code without redundant comments, optimized for advanced users.

☕ Support the Project

Pulse was created to make users' lives easier. If you find it useful, please consider supporting its development:

👉 Buy Me A Coffee

Created with ❤️ by Carlos Corral

Pulse Active | 2026