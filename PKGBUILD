# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sergey A. <murlakatamenka@disroot.org>

pkgname=rust-analyzer
_pkgver=2024-04-29
pkgver=${_pkgver//-}
pkgrel=1
pkgdesc='Rust compiler front-end for IDEs'
arch=('x86_64')
url=https://rust-analyzer.github.io/
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'rust-src')
makedepends=('git')
source=("git+https://github.com/rust-lang/$pkgname.git#tag=$_pkgver")
b2sums=('1dc17e98ec4fb48c8c55efb35b0a2bf0b948eeafebc3d20cbb86e4f8f82941be75e344043f6db4e078423cd1de68c56064fe85ffd94bce9d1daee04e2d1f375d')

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
