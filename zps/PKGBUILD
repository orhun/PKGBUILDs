# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=zps
pkgver=2.0.0
pkgrel=1
pkgdesc="A small utility for listing and cleaning up zombie processes"
arch=('x86_64')
url="https://github.com/orhun/zps"
license=('GPL-3.0-only')
depends=('glibc')
makedepends=('cmake')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('235e31e3e19abd015e21aeb9483784658e03218381890044e0fb63f2d7687328fcebcc67812ba0a20b54600024200d36833860f4289ef7c9e374b7ecd272e57d')

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
