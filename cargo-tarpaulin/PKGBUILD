# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tarpaulin
_tag=895bd941a8e5383429b584770da720e4d4817f04
pkgver=0.29.1
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
b2sums=('38a6c7efdaf6fbb7561b0658712465ab52c91fdd6bd2e6c86c488ef94fb99f81f72b8cb6dd9cc1a5642491e94cba8021ba916837dc0c76f5f143e8b09da2a4b2')

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
