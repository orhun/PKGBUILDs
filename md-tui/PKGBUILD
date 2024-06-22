# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=md-tui
pkgver=0.8.2
pkgrel=1
pkgdesc="Markdown renderer in the terminal"
arch=('x86_64')
url="https://github.com/henriklovhaug/md-tui"
license=('AGPL-3.0-only')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('dcda51b531ebebf9967a519266565e1629176cd0d8ac1f746139f911868a6c50')
options=('!lto')

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
  install -Dm 755 "target/release/mdt" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
