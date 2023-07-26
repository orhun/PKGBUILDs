# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Attenuation <ouyangjun1999@gmail.com>

pkgname=hexyl
pkgver=0.13.1
pkgrel=1
pkgdesc='Colored command-line hex viewer'
url='https://github.com/sharkdp/hexyl'
arch=('x86_64')
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo' 'pandoc')
source=("${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha512sums=('cffa229dafe9b9b87aaa4aa54bb3cc33689a4cee17a4364f2ba393e424ee82a9f1ceaa3cc11b47d595dfbe41b8fba7f51faf53c8c883387709f977e6e10411c8')
b2sums=('466252eb24179fd330136d4b257ede9aac9f7e74d7e228656f2d2c5d3c6630bafe925155b0494a42869b0ebb8b73c3fb743e9d10d3b2ad04a59501a8b94784e2')

prepare() {
  cd ${pkgname}-${pkgver}
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd ${pkgname}-${pkgver}
  cargo build --release --frozen
  pandoc -s -f markdown -t man -o "doc/${pkgname}.1" "doc/${pkgname}.1.md"
}

check() {
  cd ${pkgname}-${pkgver}
  cargo test --frozen
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm 755 target/release/${pkgname} -t "${pkgdir}/usr/bin"
  install -Dm 644 LICENSE* -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/${pkgname}"
  install -Dm 644 "doc/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
