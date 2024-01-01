# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-run-bin
_pkgname=cargo-bin
pkgver=1.7.0
pkgrel=1
pkgdesc="Build, cache, and run CLI tools scoped in Cargo.toml"
arch=('x86_64')
url='https://github.com/dustinblackman/cargo-run-bin'
license=('MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('97e202125f40753a2a2cc40fe3d4d96dedf9d3ead98cae3f7b2cfbe93da2fbce')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

# <https://github.com/dustinblackman/cargo-run-bin/issues/18>
# check() {
#   cd "$pkgname-$pkgver"
#   cargo test --frozen
# }

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
