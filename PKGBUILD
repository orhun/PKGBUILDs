# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-edit
pkgver=0.12.2
pkgrel=1
pkgdesc='Managing cargo dependencies from the command line'
url='https://github.com/killercup/cargo-edit/releases'
arch=('x86_64')
license=('MIT' 'APACHE')
depends=('cargo' 'libgit2.so' 'libssh2' 'openssl')
source=(https://github.com/killercup/${pkgname}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('91750b1129eebbbc86d9eb1e3e3ed428039b4997975a7708acee60cd537b5daa4a1de0ed64462162fa82b73a15795c1e1603aaac2f7bcc1570ec83c147f0c207')
b2sums=('37e91b5eb41fd56e2be382ee77bd6a6c859d1e1d7c99d45c2597e1a24194ea79ad1c563eb065615bf9cd87ab108de84d772e31d4faeaa57f9f556d6eb7fe570b')

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
