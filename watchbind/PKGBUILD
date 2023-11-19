# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=watchbind
pkgver=0.2.0
pkgrel=1
pkgdesc="Turn any shell command into a powerful TUI with custom keybindings"
arch=('x86_64')
url="https://github.com/fritzrehde/watchbind"
license=('GPL3')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('a4e38d05b09a8980c6924188ed853d5060d86ac8974cd9a6204a3caf1e4c031a')

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
