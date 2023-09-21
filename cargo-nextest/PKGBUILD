# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-nextest
pkgver=0.9.58
pkgrel=1
pkgdesc="A next-generation test runner for Rust."
arch=('x86_64')
url="https://github.com/nextest-rs/nextest"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/cargo-nextest-$pkgver.tar.gz")
sha256sums=('fb8ebd018cf0717067551d5e9428991207575b3c6536832f201853653b770307')
b2sums=('69c02a641704f4520fd8626fa939ce2c2698f49f37a61d578468d807762b54d854c1202d53f4dca49c392c2a0a5c77c7b6206bc6f1e1ecad8ae81380b82c3949')
options=('!lto')

prepare() {
  mv "nextest-$pkgname-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --package "$pkgname" --no-default-features --features default-no-update
}

check() {
  cd "$pkgname-$pkgver"
  cargo run --package cargo-nextest -- nextest run
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
