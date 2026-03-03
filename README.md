# ⚡ Pulse - System Monitor v1.0

Pulse es un monitor de sistema profesional, minimalista y de alto rendimiento para la terminal. Ha sido diseñado bajo una estética refinada (Expert Mode) para ofrecer una visualización clara de las métricas críticas del hardware con un impacto mínimo en los recursos del sistema.

## ✨ Características Principales
- **Telemetría en Tiempo Real**: Monitoreo dinámico de carga de CPU, frecuencia actual (MHz), uso de memoria RAM, estado de almacenamiento y tráfico de red.
- **Detección Avanzada de Hardware**: Lógica mejorada para la identificación precisa de diversas arquitecturas de GPU (gráficos integrados y dedicados) y procesadores modernos.
- **Gráficos Dinámicos**: Historial visual de la carga de CPU integrado directamente en la interfaz mediante caracteres de bloque.
- **Diseño Optimizado**: Interfaz adaptada para terminales modernas, recomendada para fondos **Dark Blue** (Azul Oscuro).

## 🚀 Instalación y Configuración

Para una integración profesional en sistemas GNU/Linux, se recomienda instalar Pulse en el directorio de binarios del usuario para que sea accesible de forma global.

### 1. Requisitos del Sistema
Asegúrate de tener instaladas las dependencias necesarias para la detección de hardware y cálculos de precisión:
```bash
sudo apt update && sudo apt install pciutils bc x11-utils -y

2. Despliegue en el Sistema

Sigue estos pasos para instalar el binario en tu carpeta local de forma correcta:
Bash

# Crear la carpeta de binarios local si no existe
mkdir -p ~/.local/bin

# Copiar el script a la carpeta de binarios
# (Asegúrate de ejecutar este comando desde donde descargaste el archivo)
cp pulse ~/.local/bin/

# Otorgar permisos de ejecución al binario
chmod +x ~/.local/bin/pulse

3. Configuración del PATH

Para ejecutar pulse simplemente escribiendo su nombre desde cualquier ubicación, añade la siguiente línea al final de tu archivo ~/.bashrc:
Bash

export PATH="$HOME/.local/bin:$PATH"

Tras guardar los cambios, reinicia tu terminal o aplica la configuración con source ~/.bashrc.
🛠️ Especificaciones Técnicas

    Fuente de Datos: Extracción eficiente de métricas directamente desde /proc/stat y /proc/net/dev.

    Motor de Renderizado: Desarrollado íntegramente en Bash utilizando secuencias de escape ANSI para máxima compatibilidad y velocidad.

    Arquitectura: Código limpio sin comentarios redundantes, optimizado para entornos de usuario avanzado.

❤️ Apoya el Proyecto

Pulse es un proyecto creado para hacer la vida de los usuarios más fácil. Si te resulta útil, puedes apoyar su desarrollo invitándome a un café:

Link de donación: https://ko-fi.com/retrolcdclock

Created by Carlos Corral | Pulse Active | 2026