# Maintainer: Filipe Laíns (ffy00) <lains@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

_pkgname=coreutils
pkgname=uutils-$_pkgname
pkgver=0.0.27
pkgrel=1
pkgdesc='Cross-platform Rust rewrite of the GNU coreutils'
arch=('x86_64')
url='https://uutils.github.io/'
_url='https://github.com/uutils/coreutils'
license=('MIT')
depends=('glibc' 'gcc-libs' 'oniguruma')
makedepends=('rust' 'cargo' 'python-sphinx')
source=("$pkgname-$pkgver.tar.gz::$_url/archive/$pkgver.tar.gz")
sha512sums=('100aa23f25d3a19c561c73d1ec8a953efabf069f7903494f2af8fe049a2820b3458f6acdfdc911c27c4636d962fdc3efaf98f71b348838f0d4cd34174d4d7373')
options=('!lto')

prepare() {
  cd $_pkgname-$pkgver
  sed 's|"bin"|"builduser"|g' -i tests/by-util/test_{chgrp,chown}.rs
}

build() {
  cd $_pkgname-$pkgver

  export RUSTONIG_DYNAMIC_LIBONIG=1
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
