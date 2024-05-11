# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tarpaulin
_tag=8d7ad30ea170dfe078aa18ed72f85bd149b971bc
pkgver=0.30.0
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
b2sums=('a5a07accc015520ea2b0047e821c0df341122244d03d02b3fd4bf874d5503a8688fc4d14ea3b515b10aec1cdb8b3b15c95b9f184e63827cc3bc8551136a7b5cc')

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
