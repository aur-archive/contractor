# Maintainer: Maxime Gauduin <alucryd@archlinux.org>

pkgname=contractor
pkgver=0.3.1
pkgrel=1
pkgdesc='A service for sharing data between apps'
arch=('i686' 'x86_64')
url="https://launchpad.net/${pkgname}"
license=('GPL3')
depends=('libgee')
makedepends=('bzr' 'cmake' 'vala')
optdepends=('brasero: Burn Disc context menu entries'
            'file-roller: Archive context menu entries'
            'gnome-bluetooth: Bluetooth context-menu entry'
            'inkscape: Inkscape context menu entry')
source=("https://launchpad.net/${pkgname}/0.3/${pkgver}/+download/${pkgname}-${pkgver}.tar.gz"
        'bzr+lp:~elementary-os/contractor/elementary-contracts')
sha256sums=('96806a7a1c206df72118320bbb6d337f003684fd085ebe68cd37c44553f45ef9'
            'SKIP')

build() {
  cd ${pkgname}-${pkgver}

  if [[ -d build ]]; then
    rm -rf build
  fi
  mkdir build && cd build

  cmake .. -DCMAKE_INSTALL_PREFIX='/usr'
  make
}

package() {
  cd ${pkgname}-${pkgver}/build

  make DESTDIR="${pkgdir}" install

  install -dm 755 "${pkgdir}"/usr/share/contractor
  for _app in brasero file-roller gnome-{bluetooth,wallpaper} inkscape; do
    install -m 644 "${srcdir}"/elementary-contracts/${_app}/*.contract "${pkgdir}"/usr/share/contractor/
  done
  install -dm 755 "${pkgdir}"/usr/lib/svg-contracts
  install -m 755 "${srcdir}"/elementary-contracts/inkscape/inkscape-export.sh "${pkgdir}"/usr/lib/svg-contracts
}

# vim: ts=2 sw=2 et:
