# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mohammadreza Abdollahzadeh <morealaz at gmail dot com>
# Contributor: Grey Christoforo <first name at last name dot net>

pkgname=wasm-bindgen
pkgver=0.2.88
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
sha256sums=('8e144b29ecd2744877431e94284ffe8a7f58a55494acca49ed18e60d829cae0b'
            'dd378a92de1eea2668116a0707f0304187596983c0b36bb61ec9a1b200207c3c')
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
