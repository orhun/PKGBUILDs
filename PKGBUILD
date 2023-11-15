# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.25.4
pkgrel=1
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('openssl' 'libcurl.so' 'libgit2.so')
makedepends=('cargo' 'clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz")
sha512sums=('6bba9892e6282e8c98b3d65230c4dd80a1c794af955864b73149cf50fc1dc9acc3f2293114952ea0110482880cd12b7c7a7dccd0da5256c7d700609c7bbef758')
b2sums=('433f0e7be836ddafc34c11e763dccef155fb48553e768f025326e4457307eb7885ae4257e7ab3140ad3c11217c7b5ddb83015e73b84bec2f000070bab1dca05f')

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
