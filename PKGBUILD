# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jonas Malaco <jonas@protocubo.io>

pkgname=cargo-show-asm
_binname=cargo-asm
pkgver=0.2.23
pkgrel=2
pkgdesc='Cargo subcommand to display ASM, LLVM-IR and MIR for Rust source code'
arch=('x86_64')
url='https://github.com/pacak/cargo-show-asm'
license=('Apache' 'MIT')
depends=('cargo' 'rust-src' 'gcc-libs')
conflicts=('cargo-asm')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('db9ab7fb3d47c1bafd21f9d7cacb0be26e54406d119d3f6988b5b634879282ed')

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
  install -Dm 755 "target/release/$_binname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
