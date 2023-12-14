# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Bert Peters <bert@bertptrs.nl>

pkgname=cargo-geiger
pkgver=0.11.7
pkgrel=1
pkgdesc="Detects usage of unsafe Rust in a Rust crate and its dependencies"
arch=('x86_64')
url="https://github.com/rust-secure-code/cargo-geiger"
license=('MIT' 'Apache')
depends=('openssl' 'curl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname@v$pkgver.tar.gz")
sha256sums=('6ddc447b0b8a46ee2b303897fbe2d416df794942cd23984c44b0ee69c4675bad')
options=('!lto')

prepare() {
  mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver/$pkgname"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver/$pkgname"
  install -Dm755 "../target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
