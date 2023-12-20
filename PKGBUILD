# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-msrv
pkgver=0.15.1
pkgrel=4
pkgdesc="Find the minimum supported Rust version (MSRV) for your project"
arch=('x86_64')
url="https://github.com/foresterre/cargo-msrv"
license=('MIT' 'Apache')
depends=('gcc-libs' 'openssl' 'rustup')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('58c54cc718cfe9653a0b506b9f85eb688583e0aa4a8b8df02738050b69460762')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all -- --test-threads=1
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  depends+=('rustup')
}

# vim:set ts=2 sw=2 et:
