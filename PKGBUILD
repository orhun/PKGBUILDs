# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=watchbind
pkgver=0.2.1
pkgrel=1
pkgdesc="Turn any shell command into a powerful TUI with custom keybindings"
arch=('x86_64')
url="https://github.com/fritzrehde/watchbind"
license=('GPL3')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('af91b06f03184487f0b8dd2d430c8bef0d65c1ff4d71652865d4cb2d24f1bd23')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
