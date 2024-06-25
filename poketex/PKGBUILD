# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=poketex
pkgver=1.13.0
pkgrel=1
pkgdesc="Simple Pokedex based on TUI"
arch=('x86_64')
url="https://github.com/ckaznable/poketex"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('a7c0643005069a5feb87af85beacb3ce7e40f9d5ad71f26c5a3e5be62fd00156')

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
