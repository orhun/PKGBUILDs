# Maintainer: Filipe Laíns (ffy00) <lains@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

_pkgname=coreutils
pkgname=uutils-$_pkgname
pkgver=0.0.19
pkgrel=1
pkgdesc='Cross-platform Rust rewrite of the GNU coreutils'
arch=('x86_64')
url='https://github.com/uutils/coreutils'
license=('MIT')
depends=('glibc' 'gcc-libs')
makedepends=('rust' 'cargo' 'python-sphinx')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('6130c4d7ca8a31c95a15b0e5e64cc69ff21e4417fe118d04c354a30933379a99334c87416418ca29f5e31f25f689686d83329f971e970c1802aa5de933ad1207')
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
