# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-depgraph
pkgver=1.5.0
pkgrel=2
pkgdesc="Creates dependency graphs for cargo projects using cargo metadata and graphviz"
arch=('x86_64')
url="https://github.com/jplatte/cargo-depgraph"
license=('GPL3')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('4213a4c8ea1436fdef524fb92b98f0bb59af86b1ff428b8c89cc9950173749a7')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim:set ts=2 sw=2 et:
