# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=typos
pkgver=1.15.1
pkgrel=1
pkgdesc="Source code spell checker"
arch=('x86_64')
url="https://github.com/crate-ci/typos"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('46f343fe709bd0aa3f2404fb5c50b43b8e344b8bab857534fe4d88b87d47580d')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${pkgname}-${pkgver}"
  cargo build --release --frozen
}

check() {
  cd "${pkgname}-${pkgver}"
  cargo test --frozen
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" -t "${pkgdir}/usr/bin"
  install -Dm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "LICENSE-MIT"    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE-MIT"
}

# vim: ts=2 sw=2 et:
