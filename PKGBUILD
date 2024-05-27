# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-05-27
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=('x86_64')
url=https://rust-analyzer.github.io/
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'rust-src')
makedepends=('git')
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('6eb2f3873bb5199b6d679fd37d550dfab70fb72873780b42b7b186c3a8958e14a684c73fa8c66de5b4545ac101a405e816bfa19c9af0dc331953b5e1f0c04091')

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
