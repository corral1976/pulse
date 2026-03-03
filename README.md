# ⚡ Pulse - System Monitor v1.0

Pulse es un monitor de sistema minimalista y de alto rendimiento para la terminal. Diseñado bajo una estética refinada, ofrece una visualización clara de las métricas críticas del hardware con un consumo de recursos despreciable.

## ✨ Características Principales
- [cite_start]**Telemetría en Tiempo Real**: Monitoreo de carga de CPU, frecuencia actual (MHz), uso de RAM, estado del disco y tráfico de red[cite: 1, 5, 11, 13, 18].
- [cite_start]**Detección Avanzada de GPU**: Lógica mejorada para identificar correctamente gráficas **AMD Radeon Vega** (especialmente en APUs como el Ryzen 7 5700G) y procesadores modernos[cite: 3].
- [cite_start]**Gráficos Dinámicos**: Historial visual de carga de CPU integrado directamente en la interfaz mediante caracteres de bloque[cite: 4, 10].
- **Diseño Optimizado**: Colores dinámicos adaptados para terminales con fondo **Dark Blue** (Azul Oscuro).

## 🚀 Instalación y Configuración

Para una integración profesional en GNU/Linux, instalaremos Pulse en el directorio de binarios del usuario para que sea accesible desde cualquier lugar.

### 1. Requisitos del Sistema
Instala las dependencias necesarias para la detección de hardware y cálculos:
```bash
sudo apt update && sudo apt install pciutils bc x11-utils -y

2. Despliegue en el Sistema

Sigue estos pasos para instalar el binario en tu carpeta local:
Bash

# Crear la carpeta de binarios local si no existe
mkdir -p ~/.local/bin

# Mover el archivo pulse a la carpeta de binarios
# (Asegúrate de estar en la carpeta donde descargaste el archivo)
cp pulse ~/.local/bin/

# Otorgar permisos de ejecución
chmod +x ~/.local/bin/pulse

3. Configuración del PATH

Para ejecutar pulse simplemente escribiendo su nombre en la terminal, añade esta línea al final de tu archivo ~/.bashrc:
Bash

export PATH="$HOME/.local/bin:$PATH"

Después de guardarlo, reinicia tu terminal o ejecuta source ~/.bashrc para aplicar los cambios.
🛠️ Especificaciones Técnicas

    Fuente de datos: Extracción directa de /proc/stat y /proc/net/dev para mínima carga.

Renderizado: Basado puramente en Bash y secuencias de escape ANSI.

Autor: Creado por Carlos Corral.

❤️ Apoya el Proyecto

Si Pulse te resulta útil y quieres apoyar su desarrollo, puedes invitarme a un café:

Link directo: https://ko-fi.com/retrolcdclock

Pulse Active | 2026
