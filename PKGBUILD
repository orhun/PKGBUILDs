# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=serpl
pkgver=0.1.28
pkgrel=1
pkgdesc="A simple TUI for search and replace, ala VS Code"
arch=('x86_64')
url="https://github.com/yassinebridi/serpl"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('c6fdace1d34e7ab216773110dfe07e3df8126443fa0a1a8f6030b099879b6aac678db4a2bfa33bb65bda7660194be6a0c5f736fbd53f473683b29f333c2a1fa3')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  VERGEN_GIT_DESCRIBE="Arch Linux" cargo build --release --frozen
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
