# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-06-03
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=('x86_64')
url=https://rust-analyzer.github.io/
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'rust-src')
makedepends=('git')
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('9d2c796b3f5f97c6fe6ab08b96c99d5d65fff05109e9896fcbea47921302fc375472bea21291ad84cd843b0bf49ef872a59960118c366023512414b063588fac')

# Use LTO
export CARGO_PROFILE_RELEASE_LTO=true CARGO_PROFILE_RELEASE_CODEGEN_UNITS=1

# Use debug
export CARGO_PROFILE_RELEASE_DEBUG=2

prepare() {
  cd $pkgname
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd $pkgname
  CFG_RELEASE=1 cargo build --release --locked --offline
}

package() {
  cd $pkgname
  install -Dt "$pkgdir"/usr/bin target/release/$pkgname
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname LICENSE-MIT
}
