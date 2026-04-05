# Maintainer: Rafael Dominiquini <rafaeldominiquini at gmail dot com>

_execname=oy
_pkgauthor=ahkohd
_pkgname=oyo

pkgname=${_pkgname}
pkgver=0.1.26
pkgrel=1
pkgdesc="A diff viewer that works two ways: step through changes or review a classic scrollable diff"

url="https://github.com/${_pkgauthor}/${pkgname}"
arch=('x86_64' 'aarch64')
license=('MIT')

depends=('glibc' 'gcc-libs')
provides=("${_execname}")
makedepends=('rust')

source=("${pkgname}-${pkgver}.tgz::https://github.com/${_pkgauthor}/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('8f98d7f50fa1026faf051802cb17ca8821974d82595ca127771ea9b4584cf11c')

build() {
	cd ${srcdir}/${pkgname}-${pkgver}/ || exit 1

	CFLAGS+=" -ffat-lto-objects" RUSTFLAGS+=" --remap-path-prefix=$(pwd)=/build/" cargo build --release --locked
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver}/ || exit 1

	install -Dm755 "target/release/${_execname}" -t "${pkgdir}/usr/bin/"

	install -Dm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
	install -Dm644 "docs/THEME.md" "${pkgdir}/usr/share/doc/${pkgname}/THEME.md"
	install -Dm644 "docs/DIFF_VIEWER.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_VIEWER.md"
	install -Dm644 "docs/DIFF_PREVIEWS.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_PREVIEWS.md"

	install -Dm644 "LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
