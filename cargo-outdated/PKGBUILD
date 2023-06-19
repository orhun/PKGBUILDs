# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jian Zeng <anonymousknight96+aur AT gmail.com>
# Contributor: Alexandre Bury <alexandre.bury+aur AT gmail.com>
# Contributor: Vlad M. <vlad@archlinux.net>

pkgname=cargo-outdated
pkgver=0.13.0
pkgrel=1
pkgdesc="A cargo subcommand for displaying when Rust dependencies are out of date"
url="https://github.com/kbknapp/cargo-outdated"
arch=('x86_64')
license=('MIT')
depends=('cargo' 'libgit2')
makedepends=('libssh2')
source=("${pkgname}-${pkgver}.tar.gz::https://crates.io/api/v1/crates/${pkgname}/${pkgver}/download")
sha256sums=('3880cd54e32364a722c1f90dd0879475cf10aa73a6eadb25c1f5b96e0380f6e9')
b2sums=('d626b01d2ea2b599271b2233c32e9bd78ebeae0fbcc7023445e7e48411891d191b5c085776d8176f835d0a2daeadda7f67a24b1460b8a3f71c8e35519397654d')
options=('!lto')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${pkgname}-${pkgver}"
  export LIBSSH2_SYS_USE_PKG_CONFIG=1
  cargo build --frozen --release
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
