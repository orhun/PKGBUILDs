# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=gping
pkgver=1.16.0
pkgrel=1
pkgdesc="Ping, but with a graph"
arch=('x86_64')
url="https://github.com/orf/gping"
license=('MIT')
depends=('iputils')
makedepends=('cargo' 'libgit2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('54b1f4a18cb3a3ad51d3dec0f1b0f8eaacaa084d1be6d4d70a2e5224b26a1032eacceb49c6755580d1370bc30a8248557c06ee3f51c5d6cf1b381cee448b8eae')
options=('!lto')

prepare() {
  mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
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
  install -Dm 644 readme.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
