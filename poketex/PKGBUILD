# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=poketex
pkgver=1.12.0
pkgrel=1
pkgdesc="Simple Pokedex based on TUI"
arch=('x86_64')
url="https://github.com/ckaznable/poketex"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('eee6036d7e6283430e8b0e9b64bbb34fcab52d08fdb38c9b928ca01fbdee5f13')

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
