# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mohammadreza Abdollahzadeh <morealaz at gmail dot com>
# Contributor: Grey Christoforo <first name at last name dot net>

pkgname=wasm-bindgen
pkgver=0.2.89
pkgrel=1
pkgdesc="Interoperating JS and Rust code"
arch=('x86_64')
url="https://github.com/rustwasm/wasm-bindgen"
license=('Apache' 'MIT')
replaces=('wasm-bindgen-cli')
depends=('rust-wasm' 'nodejs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('7d7c5b7867b12aee74abf37130b7473404f4556f366fe0572e985ca497188d3b'
            'dff0c463cee0a605b7b6fc562fb95adf26a3ae3f044e283e1d38a4d7de0e3da3')
options=('!lto')

prepare() {
  # https://github.com/rustwasm/wasm-bindgen/issues/1819
  cp Cargo.lock "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/crates/cli"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver/crates/cli"
  cargo build --frozen --release --all-features
}

check() {
  cd "$pkgname-$pkgver/crates/cli"
  cargo test --frozen --all-features
}

package() {
  cd "$pkgname-$pkgver"
  find target/release \
    -maxdepth 1 \
    -executable \
    -type f \
    -exec install -Dm0755 -t "$pkgdir/usr/bin/" {} \;
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
