# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jian Zeng <anonymousknight96+aur AT gmail.com>
# Contributor: Alexandre Bury <alexandre.bury+aur AT gmail.com>
# Contributor: Vlad M. <vlad@archlinux.net>

pkgname=cargo-outdated
pkgver=0.15.0
pkgrel=1
pkgdesc="A cargo subcommand for displaying when Rust dependencies are out of date"
url="https://github.com/kbknapp/cargo-outdated"
arch=('x86_64')
license=('MIT')
depends=(
  'cargo'
  'gcc-libs'
  'glibc'
  'libcurl.so'
  'libssh2.so'
  'libssl.so'
  'libz.so'
)
source=("${pkgname}-${pkgver}.tar.gz::https://crates.io/api/v1/crates/${pkgname}/${pkgver}/download")
sha256sums=('0641d14a828fe7dcf73e6df54d31ce19d4def4654d6fa8ec709961e561658a4d')
b2sums=('d951d3debd1ce6cbe19cc43612fcfd157bc65df075517873cb1c2e997cd5a1c502b28c2836d2cf9d68f896b1b1cf78d5c40f93efb06a72473307c806e8bd0fa6')
options=('!lto')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
