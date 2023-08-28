# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien dot nicoulaud at gmail dot com>

pkgname=lsd
pkgver=1.0.0
pkgrel=1
pkgdesc='Modern ls with a lot of pretty colors and awesome icons'
url='https://github.com/Peltoche/lsd'
arch=('x86_64')
license=('Apache')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'pandoc')
checkdepends=('git')
optdepends=(
  'nerd-fonts'
  'awesome-terminal-fonts'
)
source=(https://github.com/Peltoche/lsd/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=('ab34e9c85bc77cfa42b43bfb54414200433a37419f3b1947d0e8cfbb4b7a6325')
sha512sums=('c16fbbaa23bcc24050180d415f992459b423473eeb7771b1b8cd59aab5db97bf8d0cd01e3db507031f9588291bb8c90e02397b9a146973a054d338b60da10220')
options=('!lto')

prepare() {
  cd ${pkgname}-${pkgver}
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
