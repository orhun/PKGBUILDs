# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.24.2
pkgrel=1
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('openssl' 'libcurl.so' 'libgit2.so')
makedepends=('cargo' 'clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz")
sha512sums=('ca06382d9880221f5a402cbcd3a609b9af455a4859c004338590d5cb2c99f4a5e904667e260419e11ab58b4204f02e82576224a831d120d70f52b979e0ab097a')
b2sums=('9a673ffed9f7ed38114ea670778ad30e94e1943da750b3ebdb5ddcee50aeb13330de1f78394600ea251dc706f67503c2dcba65dd10443870bd6e129c0cb9623a')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${pkgname}-${pkgver}"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo build --frozen --release --no-default-features
}

check() {
  cd "${pkgname}-${pkgver}"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo test --frozen --no-default-features
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" -t "${pkgdir}/usr/bin"

  install -Dm644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set ts=2 sw=2 et:
