# Maintainer: Rafael Dominiquini <rafaeldominiquini at gmail dot com>

_execname=oy
_pkgauthor=ahkohd
_pkgname=oyo
pkgname=${_pkgname}
pkgver=0.1.13
pkgrel=1
pkgdesc="A step-through diff viewer"
arch=('x86_64' 'aarch64')
url="https://github.com/${_pkgauthor}/${pkgname}"
license=('MIT')

depends=('glibc' 'gcc-libs')
provides=("${_execname}")
makedepends=('rust')

source=("https://github.com/${_pkgauthor}/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('5431cee58b58ff2fc9c70c59f36036a73f737e292f2b4a393fdbf4d2cda11af4')

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
