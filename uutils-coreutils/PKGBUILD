# Maintainer: Filipe Laíns (ffy00) <lains@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

_pkgname=coreutils
pkgname=uutils-$_pkgname
pkgver=0.0.21
pkgrel=1
pkgdesc='Cross-platform Rust rewrite of the GNU coreutils'
arch=('x86_64')
url='https://github.com/uutils/coreutils'
license=('MIT')
depends=('glibc' 'gcc-libs')
makedepends=('rust' 'cargo' 'python-sphinx')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('8c5cd1c3f9f5e41016938295816bcf8bbcc6f74a121bb1ca64464bbebf0862f90929f853731b520a2e5b3c51795cbd70813509086093f6245f4f834cdb158275')
options=('!lto')

prepare() {
  cd $_pkgname-$pkgver
  sed 's|"bin"|"builduser"|g' -i tests/by-util/test_{chgrp,chown}.rs
}

build() {
  cd $_pkgname-$pkgver

  make PROFILE=release
}

# https://github.com/uutils/coreutils/issues/4946
# check() {
#   cd $_pkgname-$pkgver
#
#   make test \
#       PROFILE=release \
#       CARGOFLAGS=--release \
#       TEST_NO_FAIL_FAST="--no-fail-fast -- \
#         --skip test_chown::test_big_p \
#         --skip test_chgrp::test_big_p \
#         --skip test_chgrp::test_big_h"
# }

package() {
  cd $_pkgname-$pkgver

  make install \
      DESTDIR="$pkgdir" \
      PREFIX=/usr \
      MANDIR=/share/man/man1 \
      PROG_PREFIX=uu- \
      PROFILE=release \
      MULTICALL=y

  install -Dm 644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

# vim: ts=2 sw=2 et:
