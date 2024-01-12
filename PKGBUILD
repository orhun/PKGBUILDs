# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mohammadreza Abdollahzadeh <morealaz at gmail dot com>
# Contributor: Grey Christoforo <first name at last name dot net>

pkgname=wasm-bindgen
pkgver=0.2.90
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
sha256sums=('067c31c2f03e9c6f8365c62d162d19d00e3ebd9bd5fe95586995615c3d820514'
            '9cb3407da4f16302d19289697c80c5a2fab7ebdb649927a88f5825f893fba526')
options=('!lto')

prepare() {
  # https://github.com/rustwasm/wasm-bindgen/issues/1819
  cp Cargo.lock "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/crates/cli"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
