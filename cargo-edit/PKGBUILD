# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-edit
pkgver=0.12.1
pkgrel=1
pkgdesc='Managing cargo dependencies from the command line'
url='https://github.com/killercup/cargo-edit/releases'
arch=('x86_64')
license=('MIT' 'APACHE')
depends=('cargo' 'libgit2.so' 'libssh2' 'openssl')
source=(https://github.com/killercup/${pkgname}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('77cb2708041c4896bdb9f0afba09bd75dd028a53a80a9b5756b96f86c950f9cb44c6391d3b83e121985ca0d83f0d9b8dedfbc5c785d1ac2bb73e29e6766229e6')
b2sums=('00654c554812ed48b0b532a337e5133526ba7e07158924153f6137c5ff3329a39e6a0ee5431ab7f4ecb7c7ebd585ba054cc3d024718aa14b3232a6686bba7a0e')

prepare() {
  cd "${pkgname}-${pkgver}"
  sed -i '/\"vendored-libgit2\"/d' Cargo.toml
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd ${pkgname}-${pkgver}
  CFLAGS+=' -ffat-lto-objects'
  LIBSSH2_SYS_USE_PKG_CONFIG=1  cargo build --frozen --release
}

check() {
  cd ${pkgname}-${pkgver}
  # tests depend on target/debug/
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo test --frozen
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm 755 \
    target/release/cargo-upgrade \
    target/release/cargo-set-version \
    -t "${pkgdir}/usr/bin"

  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
