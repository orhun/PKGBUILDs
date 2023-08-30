# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rhit
pkgver=2.0.0
pkgrel=1
pkgdesc="A nginx log explorer"
arch=('x86_64')
url="https://github.com/Canop/rhit"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('31ce2653eaad71b9395d3c58d2e42f6752a4589f04d7ffe02e7933ff93135791069803d54f22e2b32ac74580c7e6af0b3187f252754527e53c40ead8b2945435')

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
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
