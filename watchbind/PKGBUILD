# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=watchbind
pkgver=0.1.19
pkgrel=1
pkgdesc="Turn any shell command into a powerful TUI with custom keybindings"
arch=('x86_64')
url="https://github.com/fritzrehde/watchbind"
license=('GPL3')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('33180d1524dee3b78a1c2cbc6a0fe8d84253f95668eeca85b90b792d6d121779')

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
}

# vim: ts=2 sw=2 et:
