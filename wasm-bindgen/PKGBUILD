# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mohammadreza Abdollahzadeh <morealaz at gmail dot com>
# Contributor: Grey Christoforo <first name at last name dot net>

pkgname=wasm-bindgen
pkgver=0.2.92
pkgrel=1
pkgdesc="Interoperating JS and Rust code"
arch=('x86_64')
url="https://github.com/rustwasm/wasm-bindgen"
license=('Apache-2.0' 'MIT')
replaces=('wasm-bindgen-cli')
depends=('rust-wasm' 'nodejs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('dd80811dd5683f0a86a333ab1994e1b39294428cc8e3c9b55d10ffa635c81600'
            '3419a14c566339a9746cd9aa22423ae7c3ee3ca96b2def95fac48a4bc6d7c355')
options=('!lto')

prepare() {
  # https://github.com/rustwasm/wasm-bindgen/issues/1819
  cp Cargo.lock "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/crates/cli"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver/crates/cli"
  export OPENSSL_NO_VENDOR=1
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
