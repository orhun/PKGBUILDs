# Maintainer: Leonidas Spyropoulos <artafinde@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname='rustypaste-cli'
pkgdesc="A CLI tool for rustypaste"
pkgver=0.4.0
pkgrel=1
arch=('x86_64')
url="https://github.com/orhun/rustypaste-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
provides=('rpaste')
source=(${pkgname}-${pkgver}.tar.gz::"${url}/archive/v${pkgver}.tar.gz")
sha256sums=('c534d047202dcae17255a816882ac6358f82735270843f0b7ae525cc15fc2e91')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "${CARCH}-unknown-linux-gnu"
}

build(){
  cd "${pkgname}-${pkgver}"
  CFLAGS+=' -ffat-lto-objects'
  env CARGO_INCREMENTAL=0 cargo build --release --frozen
}

check(){
  cd "${pkgname}-${pkgver}"
  env CARGO_INCREMENTAL=0 cargo test --frozen
}

package() {
  cd "${pkgname}-${pkgver}"
  install -D -m755 "target/release/rpaste" "${pkgdir}/usr/bin/rpaste"
  install -D -m644 "config.toml" "${pkgdir}/usr/share/doc/rustypaste-cli/example/config.toml"
  install -D -m644 "man/rpaste.1" -t "${pkgdir}/usr/share/man/man1"
  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}

# vim:set ts=2 sw=2 et:
