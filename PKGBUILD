# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-06-10
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=('x86_64')
url=https://rust-analyzer.github.io/
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'rust-src')
makedepends=('git')
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('a60f450e41084f9afec028854da0e9fc269987a443927f105899617437040583f420bb0f66c5c78ad4b33ba092b236e58526b1c94f8a3093dc80398760c1f9c4')

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
