# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Daniel Milde <daniel at milde dot cz>

pkgname=fq
pkgver=0.7.0
pkgrel=1
pkgdesc="Tool, language and decoders for inspecting binary data"
arch=('x86_64')
url="https://github.com/wader/fq"
license=('MIT')
depends=('glibc')
checkdepends=('expect')
makedepends=('go' 'git')
source=("${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha256sums=('65d46729dd8adb20cd866268114d00aa6053ee238e07a3d7677f9aa40f0c6e4b')

prepare() {
  cd "${pkgname}-${pkgver}"
  mkdir -p dist/
}

build() {
  cd "${pkgname}-${pkgver}"
  go build \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-linkmode external -extldflags \"${LDFLAGS}\" ${_BUILDINFO}" \
    -o dist/fq \
    .
}

check() {
  cd "${pkgname}-${pkgver}"
  make test
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm 755 "dist/${pkgname}" -t "${pkgdir}/usr/bin"
  install -Dm 644 LICENSE  -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim:set ts=2 sw=2 et:
