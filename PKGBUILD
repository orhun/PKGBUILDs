# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=gping
pkgver=1.15.1
pkgrel=1
pkgdesc="Ping, but with a graph"
arch=('x86_64')
url="https://github.com/orf/gping"
license=('MIT')
depends=('iputils')
makedepends=('cargo' 'libgit2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('ce9812cf1f8746f0ca28ebeba1e9330a8256dbce24e5e0aba9b26772e4b8d3e586aafcd217c2d9643575af73fc1a62d69a95b0ef5fb21b11bc8ac2dc1e22bc99')
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
