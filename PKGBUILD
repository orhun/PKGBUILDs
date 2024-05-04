# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=netscanner
pkgver=0.4.5
pkgrel=1
pkgdesc="Network scanner"
arch=('x86_64')
url="https://github.com/Chleba/netscanner"
license=('GPL3')
depends=('gcc-libs' 'iw')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('5d5998f2fe7c58d1a02c4c35ad10de6f3a0d85a2b5e6127a0105386ecb5d5e70cfae44c18fa7547757f7e0c17d8b8c8ceaed70b2e81264858eb4a1316de4ce77')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=stable
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
