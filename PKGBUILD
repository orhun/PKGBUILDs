# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=typos
pkgver=1.18.1
pkgrel=1
pkgdesc="Source code spell checker"
arch=('x86_64')
url="https://github.com/crate-ci/typos"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('a1207e03c506c1b692ddd082c53c087018b8cd83c7282f86f9ecd8093cc1f461')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
