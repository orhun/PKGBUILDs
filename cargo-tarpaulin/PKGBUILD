# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tarpaulin
_tag=d7bb8b2fb6b8e05e52b7b1195a88f5b2babdc4f9
pkgver=0.31.0
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
b2sums=('b08e6516d0e42e965e94588b41988b12ec3a349b9e849a2fb6103ed912c8cb9c7f667f52412ba594f7bb635af4f249321683a2c3373fc9c6e2c1de728a7f8053')

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
