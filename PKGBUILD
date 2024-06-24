# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-06-24
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=(x86_64)
url=https://rust-analyzer.github.io/
license=(
  Apache-2.0
  MIT
)
depends=(
  gcc-libs
  rust-src
)
makedepends=(git)
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('20e7037fb02629cae9257b39a8c009f2a6875f734d1721931c1d06086a61235cfdda5cc7280273f6c2083184a9f257cf229e274e6fd4f180796e48a691046367')

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
