# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-ndk
pkgver=3.2.2
pkgrel=1
pkgdesc="Compile Rust projects against the Android NDK without hassle"
arch=('x86_64')
url="https://github.com/bbqsrc/cargo-ndk"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('3c9663453ff1f4d0ffe8ab7bc733923a068884d1b8396854ed2ae64e2879aa5f')

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
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
