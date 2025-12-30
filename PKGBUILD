# Maintainer: Rafael Dominiquini <rafaeldominiquini at gmail dot com>

_execname=oy
_pkgauthor=ahkohd
_pkgname=oyo

pkgname=${_pkgname}
pkgver=0.1.17
pkgrel=1
pkgdesc="A diff-erent viewer"

arch=('x86_64' 'aarch64')
license=('MIT')
url="https://github.com/${_pkgauthor}/${pkgname}"

depends=('glibc' 'gcc-libs')
provides=("${_execname}")
makedepends=('rust')

source=("https://github.com/${_pkgauthor}/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('99cf72d334fc7f8096fc46cb58bc87ab591336fc93018849d5241e2849d25617')

build() {
	cd ${pkgname}-${pkgver} || exit 1

	RUSTFLAGS="--remap-path-prefix=$(pwd)=/build/" cargo build --release --locked
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver} || exit 1

	install -Dm755 "target/release/${_execname}" -t "${pkgdir}/usr/bin/"

	install -Dm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
	install -Dm644 "docs/THEME.md" "${pkgdir}/usr/share/doc/${pkgname}/THEME.md"
	install -Dm644 "docs/DIFF_VIEWER.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_VIEWER.md"
	install -Dm644 "docs/DIFF_PREVIEWS.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_PREVIEWS.md"

	install -Dm644 "LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
