# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-dist
pkgver=0.6.3
pkgrel=1
pkgdesc="Shippable application packaging for Rust"
arch=('x86_64')
url="https://github.com/axodotdev/cargo-dist"
license=('Apache' 'MIT')
depends=('cargo' 'xz' 'bzip2')
checkdepends=('git')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('36f6f21e9de0b3a5da217c769e7ce7d098209bfed4d6b48ac3554603ef076211')
options=('!lto')

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
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
