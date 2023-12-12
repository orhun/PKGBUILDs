# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Attenuation <ouyangjun1999@gmail.com>

pkgname=hexyl
pkgver=0.14.0
pkgrel=1
pkgdesc='Colored command-line hex viewer'
url='https://github.com/sharkdp/hexyl'
arch=('x86_64')
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo' 'pandoc')
source=("${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha512sums=('770fe3db1fc10ba78cde00d727cf0494d0447e08e1e1f103bd206475c839d4d04c714b5257a3c42d2e489ce02e0b4b9b2701fb89ca9222830c87ccaa2fc8463c')
b2sums=('1c2ccbb21c7aad1d2c1daca7ed99009ec2e2a02a96dd8a73d6ba11d00291f0e81afdd790d52219406ba4571408c68a5be714f5aeb36fc74c85d2868d4e0883d4')

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
