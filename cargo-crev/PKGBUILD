# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.24.3
pkgrel=1
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('openssl' 'libcurl.so' 'libgit2.so')
makedepends=('cargo' 'clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz")
sha512sums=('b33361feea0f01e93de2eb38ec00685d0573e3150d5d2908fafeb0ebbbcd6df5e1cd33b8ba089a54955d5517f56df2a3643b90545c74bce13e8789fef5358621')
b2sums=('5e71a6e99743ff1753b479bbdbe413e6b4f2a703130cde300b69957eb66becf85b44ba612d1f1745e64f825332b74ad9cfec0150faf28624d067f9a8fbf5ea51')

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
