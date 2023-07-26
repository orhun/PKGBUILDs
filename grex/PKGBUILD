# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Martin Mariano <arch@martinmariano.com>

pkgname=grex
pkgver=1.4.2
pkgrel=1
pkgdesc="A command-line tool for generating regular expressions from user-provided input strings"
arch=('x86_64')
url="https://github.com/pemistahl/grex"
license=('Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('81027075bf795030f1579eee448f60fcdfa9ee09e68fe2bd3cda8c28b9a308dfe75fa107fa1ed6f25ab8f7c8bf84b71a65d4e452589b1dc37553033d7cfcceda')

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
