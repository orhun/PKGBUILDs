# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jian Zeng <anonymousknight96+aur AT gmail.com>
# Contributor: Alexandre Bury <alexandre.bury+aur AT gmail.com>
# Contributor: Vlad M. <vlad@archlinux.net>

pkgname=cargo-outdated
pkgver=0.14.0
pkgrel=1
pkgdesc="A cargo subcommand for displaying when Rust dependencies are out of date"
url="https://github.com/kbknapp/cargo-outdated"
arch=('x86_64')
license=('MIT')
depends=('cargo' 'libgit2')
makedepends=('libssh2')
source=("${pkgname}-${pkgver}.tar.gz::https://crates.io/api/v1/crates/${pkgname}/${pkgver}/download")
sha256sums=('3669cc1183aec2e59064d746c9bf937f603c0fbce92da139cd104c0c2909dc8a')
b2sums=('9a7cfc67427bc62c6e2f0074bee5a3e7ab707196e7c14a3e4e96b177ad73581d7c601cae88c750e4a1e377a8a4e4fd79c8b9c7bb449ac722522a33c4b9e9d94c')
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
