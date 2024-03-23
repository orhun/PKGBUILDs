# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien dot nicoulaud at gmail dot com>

pkgname=lsd
pkgver=1.1.1
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
sha256sums=('7933e196bf7b164ea8879078f8a8e87381e0c49f71867e0036c82916199aba61')
sha512sums=('7a3f517bb9d9b2f3a43989caef1b7454c99fd7a4f49a86da09a221821a78273bf6be60404288fead4a36bf8e3f88cfb38e0b601c7edd2ff98ea847ca8ac0ed01')
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
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 "completions/${pkgname}.bash" "${pkgdir}/usr/share/bash-completion/completions/${pkgname}"
  install -Dm 644 "completions/${pkgname}.fish" "${pkgdir}/usr/share/fish/vendor_completions.d/${pkgname}.fish"
  install -Dm 644 "completions/_${pkgname}" "${pkgdir}/usr/share/zsh/site-functions/_${pkgname}"
  install -Dm 644 "doc/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
