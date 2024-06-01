# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=md-tui
pkgver=0.8.1
pkgrel=1
pkgdesc="Markdown renderer in the terminal"
arch=('x86_64')
url="https://github.com/henriklovhaug/md-tui"
license=('AGPL-3.0-only')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('fa6a087e33985b3a0066e790af7be0bda8ca7a2b4a04bf74d07d89259fbf0950')
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
