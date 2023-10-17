# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.25.3
pkgrel=1
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('openssl' 'libcurl.so' 'libgit2.so')
makedepends=('cargo' 'clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz")
sha512sums=('a72ec2f3c3350fbb10c4441824d6ac7daaddac48632c038b63856faf2f0ea729ef094d483966af5fc385f075cce4ccc6c98c5f9ca772c39b35d566c8fe3cc9d8')
b2sums=('a8e1c199acee83b3f94ca7829dda20986c6dec94ecc743255ccd80d804e462c22e61c7b426767261f0ecfab9de74fdb33f73384d4a19d8a6d83297c36e321db0')

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
