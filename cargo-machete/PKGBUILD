# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-machete
pkgver=0.6.0
pkgrel=2
pkgdesc="Remove unused Rust dependencies"
arch=('x86_64')
url="https://github.com/bnjbvr/cargo-machete"
license=('MIT')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('a13fab0c5ff64907e6b39dee054e5e9c4278fbe06065ff5bfcb160a5c1d204ea')

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
 cargo test --release --locked
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
