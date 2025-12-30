# Maintainer: Rafael Dominiquini <rafaeldominiquini at gmail dot com>

_execname=oy
_pkgauthor=ahkohd
_pkgname=oyo

pkgname=${_pkgname}
pkgver=0.1.16
pkgrel=1
pkgdesc="A diff-erent viewer"

arch=('x86_64' 'aarch64')
license=('MIT')
url="https://github.com/${_pkgauthor}/${pkgname}"

depends=('glibc' 'gcc-libs')
provides=("${_execname}")
makedepends=('rust')

source=("https://github.com/${_pkgauthor}/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('c7f4ac032e13aee626df7c99249c29254fba0a20940e68365414264d68245daa')

build() {
	cd ${pkgname}-${pkgver} || exit 1

	RUSTFLAGS="--remap-path-prefix=$(pwd)=/build/" cargo build --release --locked
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver} || exit 1

	install -Dm755 "target/release/${_execname}" -t "${pkgdir}/usr/bin/"

	install -Dm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"

	install -Dm644 "LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
