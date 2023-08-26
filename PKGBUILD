# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Martin Mariano <arch@martinmariano.com>

pkgname=grex
pkgver=1.4.4
pkgrel=1
pkgdesc="A command-line tool for generating regular expressions from user-provided input strings"
arch=('x86_64')
url="https://github.com/pemistahl/grex"
license=('Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3715160417703a28447012abc70ea39548c4a3aaddebbfc6a3a6dc54dfe8f6856ffab355305f97c39add86fe81a8ce583e85c0f7bb19542fb1840f97871c5ad2')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release
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
