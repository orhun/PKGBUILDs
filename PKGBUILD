# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Martin Mariano <arch@martinmariano.com>

pkgname=grex
pkgver=1.4.5
pkgrel=1
pkgdesc="A command-line tool for generating regular expressions from user-provided input strings"
arch=('x86_64')
url="https://github.com/pemistahl/grex"
license=('Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('feac7d76d7f0a8b50377665a91aea1cf4580818d8aa6bbd86e0bfef8c8ded01d1f01613bb45d36360d6e8d142d00f2cedbe66d61518da09089852fcf75dafcc7')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
