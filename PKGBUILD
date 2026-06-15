# Maintainer: Rafael Dominiquini <rafaeldominiquini at gmail dot com>

_execname=oy
_pkgauthor=ahkohd
_pkgname=oyo

pkgname=${_pkgname}
pkgver=0.1.35
pkgrel=1
pkgdesc="A diff viewer that works two ways: step through changes or review a classic scrollable diff"

url="https://github.com/${_pkgauthor}/${pkgname}"
arch=('x86_64' 'aarch64')
license=('MIT')

depends=('glibc' 'libgcc')
provides=("${_execname}")
makedepends=('rust')

source=("${pkgname}-${pkgver}.tgz::https://github.com/${_pkgauthor}/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('fa62f3578935120fa526dd1251d5e88f5cf969b833db1217d9c3f1a65501f9ae')

build() {
	cd ${srcdir}/${pkgname}-${pkgver}/ || exit 1

	CFLAGS+=" -ffat-lto-objects" RUSTFLAGS+=" --remap-path-prefix=$(pwd)=/build/" cargo build --release --locked
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver}/ || exit 1

	install -Dm755 "target/release/${_execname}" -t "${pkgdir}/usr/bin/"

	install -Dm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
	install -Dm644 "PROFILING.md" "${pkgdir}/usr/share/doc/${pkgname}/PROFILING.md"

	install -Dm644 "docs/PERF.md" "${pkgdir}/usr/share/doc/${pkgname}/PERF.md"
	install -Dm644 "docs/THEME.md" "${pkgdir}/usr/share/doc/${pkgname}/THEME.md"
	install -Dm644 "docs/DEBUG.md" "${pkgdir}/usr/share/doc/${pkgname}/DEBUG.md"
	install -Dm644 "docs/DIFF_VIEWER.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_VIEWER.md"
	install -Dm644 "docs/DIFF_PREVIEWS.md" "${pkgdir}/usr/share/doc/${pkgname}/DIFF_PREVIEWS.md"

	install -Dm644 "LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
