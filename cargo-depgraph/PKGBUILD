# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-depgraph
pkgver=1.5.0
pkgrel=1
pkgdesc="Creates dependency graphs for cargo projects using cargo metadata and graphviz"
arch=('x86_64')
url="https://github.com/jplatte/cargo-depgraph"
license=('GPL3')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('6826402ec9b8f2e942954ae0cfe9848cc4d2aa3d98ff89bee05bdeed787d66bb')

prepare() {
  cd "$pkgname-v$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-v$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-v$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-v$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim:set ts=2 sw=2 et:
