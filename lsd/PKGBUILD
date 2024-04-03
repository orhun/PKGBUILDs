# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien dot nicoulaud at gmail dot com>

pkgname=lsd
pkgver=1.1.2
pkgrel=1
pkgdesc='Modern ls with a lot of pretty colors and awesome icons'
url='https://github.com/lsd-rs/lsd'
arch=('x86_64')
license=('Apache-2.0')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'pandoc')
checkdepends=('git')
optdepends=(
  'nerd-fonts'
  'awesome-terminal-fonts'
)
source=(https://github.com/lsd-rs/lsd/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha256sums=('cd80dae9a8f6c4c2061f79084468ea6e04c372e932e3712a165119417960e14e')
sha512sums=('2d0370c5fb463a4f5e1f2b0366e4fa4baab08eb307b8410d430361777d061a18b9bb9f75a7d19afbb12449c62a59d986cdb170937b7814f49cfbeb85612e8d54')
options=('!lto')

prepare() {
  cd ${pkgname}-${pkgver}
  cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')" # --locked
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
