# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=zps
pkgver=1.2.9
pkgrel=1
pkgdesc="A small utility for listing and cleaning up zombie processes"
arch=('x86_64')
url="https://github.com/orhun/zps"
license=('GPL3')
depends=('glibc')
makedepends=('cmake')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('fd3a7b7d15ce738687631b23cc0fe5ae52e5958102d6a940d9c0d16fefeb69fab6d8c50db26838408642151d3d6c9d8a108f41e6821421bc6469516b2645d669')

build() {
  cd "$pkgname-$pkgver"
  mkdir -p build && cd build/
  cmake ../ -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package() {
  cd "$pkgname-$pkgver/build"
  make DESTDIR="$pkgdir" install
  install -Dm 644 "../README.md" -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "../man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
  install -Dm 644 "../.application/$pkgname.desktop" -t "$pkgdir/usr/share/applications"
}

# vim: ts=2 sw=2 et:
