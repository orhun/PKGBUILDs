# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kpcyrd <git@rxv.cc>

pkgname=cargo-bloat
pkgver=0.12.1
pkgrel=1
pkgdesc="Find out what takes most of the space in your executable"
url="https://github.com/RazrFalcon/cargo-bloat"
depends=('cargo' 'gcc-libs')
arch=('x86_64')
license=('MIT')
source=("${pkgname}-${pkgver}.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('8195cebb94a740cd3b89611ae79d7d3e2d8fd8ec297f5a0f07efa7069ef05be7')

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
  install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set ts=2 sw=2 et:
