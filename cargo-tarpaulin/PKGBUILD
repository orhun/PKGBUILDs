# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tarpaulin
_tag=ddac75d2c7539498d22129af2b8c359824431fae
pkgver=0.29.2
pkgrel=1
pkgdesc="Tool to analyse test coverage of cargo projects"
arch=('x86_64')
url=https://github.com/xd009642/tarpaulin
license=('Apache-2.0' 'MIT')
depends=(
  'cargo'
  'gcc-libs'
  'glibc'
  'libcurl.so'
  'openssl'
  'libssh2'
  'libgit2'
  'zlib'
)
makedepends=('git')
source=("$pkgname-$pkgver::git+$url.git#tag=$pkgver")
b2sums=('29b63be22e330929b29f4b9b8fb5bed9488f98cd6a8f3035038d71ef7a07abe57397a2c9a0414074f1931d28d2b40c937c30900e3baa99d05a7d81efda666834')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  export LIBSSH2_SYS_USE_PKG_CONFIG=1
  CFLAGS+=" -ffat-lto-objects"
  cargo build --release --frozen 
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/${pkgname}" -t "${pkgdir}"/usr/bin/
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
