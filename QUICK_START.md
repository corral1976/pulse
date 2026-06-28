# 🚀 Pulse v1.3 - Quick Start Guide

## Installation

### Option 1: Local User Folder (Recomendado para desarrollo)
```bash
cp pulse ~/.local/bin/
chmod +x ~/.local/bin/pulse

# Asegúrate que ~/.local/bin esté en tu PATH
echo $PATH | grep -q ~/.local/bin || echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Test
pulse --version
pulse --help
```

### Option 2: System-wide Installation
```bash
sudo cp pulse /usr/local/bin/
sudo chmod +x /usr/local/bin/pulse

# Test
pulse --version
```

### Option 3: Debian/Ubuntu (si lo subes a AUR/PPA)
```bash
sudo apt install pulse-monitor  # (futuro)
```

---

## Basic Usage

### Normal mode (GUI - colored terminal)
```bash
pulse
```
- Actualiza cada 1 segundo
- Corazón ASCII colorido + métricas en tiempo real
- Presiona Ctrl+C para salir

### Normal mode (TTY - sin colores)
```bash
# En consola sin soporte X11
pulse
```
- Detecta automáticamente y usa ASCII art simple
- Funciona en SSH, tmux, screen

### Quiet mode (una línea)
```bash
pulse --quiet
```
- Salida minimalista: `[HH:MM:SS] CPU:XX%  RAM:XX%  DSK:XX%  NET D:XkB/U:XkB  CPU:XX°C`
- Sin clear de pantalla (sin parpadeo)
- Perfecta para integrar en scripts, dashboards, cron jobs

### Custom refresh interval
```bash
pulse --interval 2    # Refresh cada 2 segundos
pulse -i 5            # Refresh cada 5 segundos
```

### Monitor a specific disk
```bash
DISK_PATH=/home pulse          # Monitorear /home
DISK_PATH=/mnt/backup pulse    # Monitorear /mnt/backup
```

### Override window manager detection
```bash
WM=i3 pulse          # Si la detección automática falla
WM=kwin_wayland pulse
```

### Help & Version
```bash
pulse --help
pulse -h
pulse --version
pulse -v
```

---

## Environment Variables

| Variable | Default | Purpose |
|----------|---------|---------|
| `DISK_PATH` | `/` | Qué partición monitorear |
| `WM` | Auto-detect | Override de gestor de ventanas |
| `REFRESH_INTERVAL` | `1` | Segundos entre updates |

### Example
```bash
DISK_PATH=/home REFRESH_INTERVAL=2 pulse
```

---

## Integration Examples

### 1. Monitor en background, log a archivo
```bash
pulse --quiet --interval 5 >> ~/pulse_log.txt &
# Verifica:
tail -f ~/pulse_log.txt
```

### 2. Dashboard minimalista en tmux
```bash
# ~/.tmux.conf
set -g status-right-length 80
set -g status-right "#(pulse --quiet 2>/dev/null | tail -c 70)"
```

### 3. Notificaciones si CPU es alto
```bash
while true; do
    cpu=$(pulse --quiet 2>/dev/null | grep -oP 'CPU:\K[0-9]+')
    if [ "$cpu" -gt 80 ]; then
        notify-send "⚠️ CPU HIGH" "CPU: ${cpu}%"
    fi
    sleep 10
done
```

### 4. Exportar a Prometheus (futuro)
```bash
# pulse_exporter.sh
while true; do
    data=$(pulse --quiet)
    cpu=$(echo "$data" | grep -oP 'CPU:\K[0-9]+')
    echo "pulse_cpu_usage_percent $cpu" >> /tmp/metrics.txt
    sleep 5
done
```

---

## Troubleshooting

### "Command not found"
```bash
# Verifica que está en el PATH
which pulse
# Si no, agrega a ~/.bashrc:
export PATH="$HOME/.local/bin:$PATH"
source ~/.bashrc
```

### "Missing optional dependencies"
```bash
# Pulse te dirá qué falta:
# Nota: funciones opcionales reducidas (no instalado: sensors nvidia-smi xdpyinfo)

# Instala lo que quieras:
sudo apt install lm-sensors nvidia-utils x11-utils  # Debian/Ubuntu
sudo pacman -S lm_sensors nvidia-utils xorg-xdpyinfo  # Arch
```

### "TTY mode in GUI" o "GUI mode in TTY"
```bash
# Pulse auto-detecta. Si falla, fuerza manual:
export TERM=xterm  # Para GUI en terminal
export DISPLAY=    # Para TTY
pulse
```

### Falsos positivos en temperatura
```bash
# Si ve CPU:0°C o valores raros, probablemente sensors no está calibrado
sensors-detect  # Ejecuta una sola vez (requiere sudo)
sensors        # Verifica que funciona
```

### Batería no detectada
```bash
# Si no tienes laptop, mostrará "No Battery" (normal)
# Si tienes pero no se detecta:
ls -la /sys/class/power_supply/
upower -e
```

---

## Performance Notes

- **CPU Usage**: ~0.5-2% incluso en actualización cada 1 segundo (muy eficiente)
- **Memory**: ~1-2 MB RAM constante (gracias al cache inteligente)
- **Network Impact**: Cero (solo lee de /proc)
- **Disk I/O**: Mínimo (cache de 5-10 segundos para df/sensors)

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Salir |
| `q` | Salir (en modo GUI) |
| Cualquier otra tecla | Exit (en modo quiet) |

---

## Files Created

```
~/.local/bin/pulse              # El ejecutable
~/.config/pulse/                # (Futuro) Config file location
```

---

## Coming Soon (v1.4+)

- [ ] `--once` flag (snapshot único, no loop)
- [ ] `~/.config/pulse/config` (archivo de config persistente)
- [ ] Soporte `NO_COLOR` env var
- [ ] Estadísticas históricas (top 5 CPU peaks)
- [ ] Exporta a JSON para parseo fácil
- [ ] Modo Prometheus exporter

---

## Contributing / Reporting Bugs

Si encuentras un bug o tienes sugerencias:

1. Verifica que tienes v1.3+:
   ```bash
   pulse --version
   ```

2. Recopila info:
   ```bash
   pulse --help
   cat /etc/os-release
   uname -a
   ```

3. Reporta en GitLab: https://gitlab.com/corral1976/pulse

---

## Credits

- **Author**: Carlos Corral | Pulse Active
- **License**: MIT
- **Donate**: https://ko-fi.com/retrolcdclock

Enjoy monitoring! 💚
