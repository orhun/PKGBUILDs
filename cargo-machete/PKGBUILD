# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-machete
pkgver=0.5.0
pkgrel=1
pkgdesc="Remove unused Rust dependencies"
arch=('x86_64')
url="https://github.com/bnjbvr/cargo-machete"
license=('MIT')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('17dec610b7e3c246bdda53e21c6f54a4eda6925981079ce068f21455eae27a86')

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
