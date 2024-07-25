# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=md-tui
pkgver=0.8.3
pkgrel=1
pkgdesc="Markdown renderer in the terminal"
arch=('x86_64')
url="https://github.com/henriklovhaug/md-tui"
license=('AGPL-3.0-only')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('98ad8cd5a49aae813e734d3158f15f2429fb0cb7adc299f703a4fbfec14c35ba')
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
