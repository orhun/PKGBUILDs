# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=zenith
pkgver=0.14.1
pkgrel=1
pkgdesc="Terminal system monitor with histograms"
arch=('x86_64')
url="https://github.com/bvaisvil/zenith"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'clang')
optdepends=('nvidia-utils')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('73d704b3cbf93506c22f3a7d98ae1a75011434a27a978dd0a7b6b30c7794423b')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 "README.md" -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "assets/$pkgname.desktop" -t "$pkgdir/usr/share/applications"
  install -Dm 644 "assets/$pkgname.png" -t "$pkgdir/usr/share/pixmaps"
}

# vim: ts=2 sw=2 et:
