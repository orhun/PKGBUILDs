# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=bugstalker
_pkgname=BugStalker
pkgver=0.2.0
pkgrel=1
pkgdesc="Rust debugger for Linux x86-64"
arch=('x86_64')
url="https://github.com/godzie44/BugStalker"
license=('MIT')
depends=('gcc-libs' 'libunwind')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('0bbc595a33aa515333d3bf99eb86e07e86d5b375050ba6ee75032f133ac6bea63d263d3e87b30162970d528fd70402a7c0fed7cad656cc5469c59616a56e5553')
options=('!lto')

prepare() {
  mv "$_pkgname-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/bs" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
