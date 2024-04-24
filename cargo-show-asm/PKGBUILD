# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jonas Malaco <jonas@protocubo.io>

pkgname=cargo-show-asm
_binname=cargo-asm
pkgver=0.2.33
pkgrel=1
pkgdesc='Cargo subcommand to display ASM, LLVM-IR and MIR for Rust source code'
arch=('x86_64')
url='https://github.com/pacak/cargo-show-asm'
license=('Apache-2.0' 'MIT')
depends=('cargo' 'rust-src' 'gcc-libs')
conflicts=('cargo-asm')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('0751af08a6a16eea538eb68e80c31726ed9c31c68a38f4ac0944332d670d2f40')

prepare() {
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
  install -Dm 755 "target/release/$_binname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
