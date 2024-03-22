# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien dot nicoulaud at gmail dot com>

pkgname=lsd
pkgver=1.1.0
pkgrel=1
pkgdesc='Modern ls with a lot of pretty colors and awesome icons'
url='https://github.com/Peltoche/lsd'
arch=('x86_64')
license=('Apache-2.0')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'pandoc')
checkdepends=('git')
optdepends=(
  'nerd-fonts'
  'awesome-terminal-fonts'
)
source=(https://github.com/Peltoche/lsd/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=('4bbd180deeef2674e55724bb4297ee0442bea956e36f9c4cd2fcca4e82bb4026')
sha512sums=('4e6a80c03dc5ac65e47eb843323361a75d1eb2c98deb46f0c3075144d0af5ee1d75387580f80c50643b4f176ddd5229b9e3c0b07e6709a03a1b0256f0df9c286')
options=('!lto')

prepare() {
  cd ${pkgname}-${pkgver}
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd ${pkgname}-${pkgver}
  SHELL_COMPLETIONS_DIR=completions cargo build --release --frozen
  pandoc "doc/$pkgname.md" --standalone --to=man -o "doc/$pkgname.1"
}

check() {
  cd ${pkgname}-${pkgver}
  cargo test --frozen
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm 755 target/release/${pkgname} -t "${pkgdir}/usr/bin"
  install -Dm 644 README.md CHANGELOG.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 "completions/${pkgname}.bash" "${pkgdir}/usr/share/bash-completion/completions/${pkgname}"
  install -Dm 644 "completions/${pkgname}.fish" "${pkgdir}/usr/share/fish/vendor_completions.d/${pkgname}.fish"
  install -Dm 644 "completions/_${pkgname}" "${pkgdir}/usr/share/zsh/site-functions/_${pkgname}"
  install -Dm 644 "doc/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
