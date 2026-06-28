# 📦 Pulse v1.3 - PKGBUILD para AUR (Arch User Repository)

> Guía para empaquetar Pulse y publicarlo en el AUR, para que usuarios de Arch Linux puedan instalarlo fácilmente.

---

## ¿Qué es AUR?

El **AUR (Arch User Repository)** es el repositorio comunitario de Arch Linux, donde cualquiera puede publicar PKGBUILDs.

- **Ventaja**: Los usuarios hacen `yay -S pulse-monitor` o `makepkg` sin tocar archivos
- **Audiencia**: Comunidad Arch Linux (y derivadas: Manjaro, EndeavourOS, etc.)
- **Mantenimiento**: Tú controlas las actualizaciones

---

## Paso 1: Preparar el PKGBUILD

Crea el archivo `PKGBUILD` en la raíz de tu repo:

```bash
cat > PKGBUILD << 'EOF'
# Maintainer: Carlos Corral <corral1976@gmail.com>

pkgname=pulse-monitor
pkgver=1.3
pkgrel=1
pkgdesc="A minimalist and elegant system monitor for the terminal"
arch=('any')
url="https://gitlab.com/corral1976/pulse"
license=('MIT')
depends=('bash>=4.0')
optdepends=(
    'lm_sensors: CPU/GPU temperature monitoring'
    'nvidia-utils: NVIDIA GPU temperature'
    'mesa: GPU information (glxinfo)'
    'pciutils: GPU model name fallback'
    'upower: Battery status'
    'xorg-xdpyinfo: Display resolution'
    'procps-ng: System utilities'
)
source=("$url/-/archive/v$pkgver/pulse-v$pkgver.tar.gz")
sha256sums=('REPLACE_WITH_ACTUAL_SHA256')

package() {
    cd "$srcdir"
    install -Dm755 "pulse" "$pkgdir/usr/bin/pulse"
    install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 "README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
}
EOF
```

### Explicación de los campos

| Campo | Valor | Nota |
|-------|-------|------|
| `pkgname` | `pulse-monitor` | Nombre en AUR (único) |
| `pkgver` | `1.3` | Versión actual |
| `pkgrel` | `1` | Revisión (1 = primera vez) |
| `pkgdesc` | Descripción corta | <80 caracteres |
| `arch` | `('any')` | Script bash, funciona en cualquier arch |
| `url` | Repo GitLab | Fuente oficial |
| `license` | `('MIT')` | Tu licencia |
| `depends` | `('bash>=4.0')` | Requisitos obligatorios |
| `optdepends` | Lista | Mejoran funcionalidad pero no rompen nada |
| `source` | URL del tarball | GitLab/GitHub archive URL |
| `sha256sums` | Hash SHA256 | Para verificar integridad |

---

## Paso 2: Obtener el SHA256

```bash
# Descargar el archivo y calcular su hash
cd /tmp
wget "https://gitlab.com/corral1976/pulse/-/archive/v1.3/pulse-v1.3.tar.gz"
sha256sum pulse-v1.3.tar.gz
# Copiar el resultado (primer campo) al PKGBUILD
```

**Ejemplo**:
```bash
d4c8f9e2a1b3c5f7... (56 caracteres)
```

Actualiza el `PKGBUILD`:
```bash
sha256sums=('d4c8f9e2a1b3c5f7...')
```

---

## Paso 3: Probar el PKGBUILD localmente

```bash
# En el directorio con tu PKGBUILD
makepkg -si

# Flags:
# -s: Instala dependencias automáticamente
# -i: Instala después de compilar
# -r: Limpia directorios de construcción

# Verificar que funciona
pulse --version
```

Si falla, revisa el error y ajusta el PKGBUILD.

---

## Paso 4: Actualizar el Archivo .SRCINFO

El archivo `.SRCINFO` contiene metadatos que AUR parsea automáticamente:

```bash
makepkg --printsrcinfo > .SRCINFO
```

Esto genera:
```
pkgbase = pulse-monitor
    pkgdesc = A minimalist and elegant system monitor...
    pkgver = 1.3
    arch = any
    url = https://gitlab.com/corral1976/pulse
    license = MIT
    depends = bash>=4.0
    optdepends = ...
```

---

## Paso 5: Crear la Cuenta en AUR

1. Ve a https://aur.archlinux.org/
2. Click en "Register"
3. Crea usuario + contraseña
4. Confirma email

---

## Paso 6: Configurar SSH Keys (Autenticación)

AUR usa SSH para push (no HTTPS).

```bash
# Generar clave SSH si no la tienes
ssh-keygen -t ed25519 -C "corral1976@gmail.com"
# Guarda en ~/.ssh/id_ed25519

# Agregar clave pública a AUR
cat ~/.ssh/id_ed25519.pub
# Copia el contenido y pégalo en AUR → Account Settings → SSH Public Keys

# Test SSH
ssh aur@aur.archlinux.org
# Debe decir: "welcome to the AUR" y desconectarse (es normal)
```

---

## Paso 7: Clonar el Repositorio Inicial

```bash
# Reemplaza con tu usuario AUR
git clone ssh://aur@aur.archlinux.org/pulse-monitor.git
cd pulse-monitor
```

Si es la primera vez, el repo estará vacío. Es normal.

---

## Paso 8: Agregar Archivos y Hacer Commit

```bash
cp /ruta/a/tu/PKGBUILD .
cp /ruta/a/tu/.SRCINFO .

git add PKGBUILD .SRCINFO
git commit -m "Initial commit: pulse-monitor v1.3"
```

### Mensaje de Commit Recomendado

```
pulse-monitor: Initial commit (v1.3)

- Minimalist system monitor for terminal
- Dual-mode: GUI (colors) and TTY (ASCII)
- Real-time CPU/RAM/disk/network metrics
- Intelligent caching for performance
```

---

## Paso 9: Hacer Push a AUR

```bash
git push origin master
```

¡Listo! Tu PKGBUILD está ahora en AUR.

---

## Paso 10: Mantener Actualizado

Cuando hayas una nueva versión (ej. v1.4):

1. Actualiza el PKGBUILD:
   ```bash
   pkgver=1.4
   pkgrel=1  # Resetear a 1 si cambia pkgver
   # Calcula nuevo sha256sum
   sha256sums=('nuevo_hash...')
   ```

2. Regenera `.SRCINFO`:
   ```bash
   makepkg --printsrcinfo > .SRCINFO
   ```

3. Commit y push:
   ```bash
   git add PKGBUILD .SRCINFO
   git commit -m "pulse-monitor: Update to v1.4"
   git push
   ```

---

## PKGBUILD Completo (Plantilla Final)

```bash
# Maintainer: Carlos Corral <corral1976@gmail.com>
# Contributor: [otro mantenedor si lo hay]

pkgname=pulse-monitor
pkgver=1.3
pkgrel=1
pkgdesc="A minimalist and elegant system monitor for the terminal, designed for advanced GNU/Linux users"
arch=('any')
url="https://gitlab.com/corral1976/pulse"
license=('MIT')
depends=('bash>=4.0')
optdepends=(
    'lm_sensors: CPU/GPU temperature monitoring'
    'nvidia-utils: NVIDIA GPU temperature'
    'mesa: GPU information via glxinfo'
    'pciutils: GPU model name fallback'
    'upower: Battery status information'
    'xorg-xdpyinfo: Display resolution detection'
    'procps-ng: Process utilities for system info'
)
source=("$url/-/archive/v$pkgver/pulse-v$pkgver.tar.gz")
sha256sums=('PLACEHOLDER_SHA256')

package() {
    cd "$srcdir/pulse-v$pkgver"
    
    # Install binary
    install -Dm755 "pulse" "$pkgdir/usr/bin/pulse"
    
    # Install license
    install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    
    # Install documentation
    install -Dm644 "README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
}
```

---

## Ejemplo de .SRCINFO Generado

```
pkgbase = pulse-monitor
	pkgdesc = A minimalist and elegant system monitor for the terminal, designed for advanced GNU/Linux users
	pkgver = 1.3
	pkgrel = 1
	url = https://gitlab.com/corral1976/pulse
	arch = any
	license = MIT
	depends = bash>=4.0
	optdepends = lm_sensors: CPU/GPU temperature monitoring
	optdepends = nvidia-utils: NVIDIA GPU temperature
	optdepends = mesa: GPU information via glxinfo
	optdepends = pciutils: GPU model name fallback
	optdepends = upower: Battery status information
	optdepends = xorg-xdpyinfo: Display resolution detection
	optdepends = procps-ng: Process utilities for system info
	source = https://gitlab.com/corral1976/pulse/-/archive/v1.3/pulse-v1.3.tar.gz
	sha256sums = PLACEHOLDER_SHA256

pkgname = pulse-monitor
```

---

## Instalación desde AUR (Usuario Final)

Una vez publicado en AUR, cualquier usuario Arch puede instalar:

```bash
# Con yay (helper más popular)
yay -S pulse-monitor

# Con paru (alternativa)
paru -S pulse-monitor

# O compilar manualmente
git clone https://aur.archlinux.org/pulse-monitor.git
cd pulse-monitor
makepkg -si
```

---

## Buenas Prácticas AUR

### ✅ DO

- **Nombra el PKGBUILD claramente**: `pulse-monitor`, no `pulse` (para evitar conflictos)
- **Usa dependencias opcionales**: Permite instalación mínima
- **Documenta en el `pkgdesc`**: Explica qué hace, no solo "monitor"
- **Mantén `pkgrel` consistente**: Incrementa si cambias PKGBUILD pero no pkgver
- **Prueba `makepkg` antes de publicar**: `makepkg -si` siempre funcione
- **Incluye archivos de licencia**: Requisito AUR
- **Escucha comentarios**: Los usuarios pueden dar feedback en AUR

### ❌ DON'T

- **No nombres `pulse`** (conflicto potencial con otros paquetes)
- **No subas binarios compilados** (AUR compila desde fuente)
- **No uses referencias relativas en `source`** (siempre URLs)
- **No olvides actualizar `.SRCINFO`** (AUR lo regenera pero mejor proactivo)
- **No hagas cambios sin notificar** (si hay otros mantenedores)

---

## Troubleshooting

### "makepkg: unknown key in PKGBUILD"
```bash
# Revisa sintaxis bash
bash -n PKGBUILD
```

### "Invalid or missing PGP signature"
```bash
# Ignora si no usas firmas GPG (es opcional para nuevos PKGs)
makepkg -si --skippgpcheck
```

### "Source file not found"
```bash
# Verifica URL en `source` es válida
# Descarga manualmente: wget $source_url
```

### El paquete funciona localmente pero AUR reporta error
```bash
# AUR usa binarios diferentes (maybe different bash version)
# Prueba en contenedor Arch:
docker run -it archlinux bash
cd /tmp && makepkg -si
```

---

## Próximos Pasos (Opcional)

### 1. Crear Repositorio Oficial
Si tienes muchos paquetes, considera un repositorio `.pkg.tar.zst` privado:
```bash
# Hospedar en tu servidor, usar pacman -U para instalar
```

### 2. Notariar Releases en GitLab
```bash
git tag -s v1.3 -m "Release 1.3"
git push origin --tags
```

### 3. CI/CD para Validar PKGBUILD
```yaml
# .gitlab-ci.yml
test:
  image: archlinux:latest
  script:
    - pacman -Syu --noconfirm base-devel
    - makepkg -si
    - pulse --version
```

---

## Contacto & Soporte AUR

- **Comentarios en AUR**: https://aur.archlinux.org/packages/pulse-monitor
- **Reportar bugs**: Usa `git notes` o comenta en AUR
- **Solicitudes de fusión**: GitLab (tu repo oficial)

---

## Referencias

- [AUR Submission Guidelines](https://wiki.archlinux.org/title/AUR_submission_guidelines)
- [PKGBUILD Manual](https://wiki.archlinux.org/title/PKGBUILD)
- [Arch Package Guidelines](https://wiki.archlinux.org/title/Arch_package_guidelines)
- [Creating Packages](https://wiki.archlinux.org/title/Creating_packages)

---

**¡A publicar en AUR! 🚀**

Con tu PKGBUILD listo, la comunidad Arch tendrá acceso fácil a Pulse.
