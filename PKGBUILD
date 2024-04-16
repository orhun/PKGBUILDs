# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=poketex
pkgver=1.12.2
pkgrel=1
pkgdesc="Simple Pokedex based on TUI"
arch=('x86_64')
url="https://github.com/ckaznable/poketex"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('c7fbff0babf6e19e5940ced2c2c0ed3a1f44d9d531bab5ea5510fc610da3c74b')

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
  install -Dm 644 colorscripts/small/regular/* -t "$pkgdir/usr/share/$pkgname/colorscripts/small/regular"
  install -Dm 644 colorscripts/small/shiny/* -t "$pkgdir/usr/share/$pkgname/colorscripts/small/shiny"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
