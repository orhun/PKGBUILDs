# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-04-01
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=('x86_64')
url=https://rust-analyzer.github.io/
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'rust-src')
makedepends=('git')
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('48bf92212058a44ebd7b5fcb9d2db2df3575192eeb2f11417c9f0043041f13daa1d57033c2b61487794f5ac8c615ad91665a8aa4fb7ca2e39cd8ad4a6d118c28')

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
