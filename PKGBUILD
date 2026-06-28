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

# Local testing (archivo directo en el repo)
source=("file://$PWD/pulse")

package() {
    install -Dm755 "$srcdir/pulse" "$pkgdir/usr/bin/pulse"
    install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
