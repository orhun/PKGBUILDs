# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=eza
pkgver=0.17.1
pkgrel=1
pkgdesc="A modern replacement for ls (community fork of exa)"
url="https://github.com/eza-community/eza"
arch=("x86_64")
license=("MIT")
provides=('exa')
replaces=('exa')
conflicts=('exa')
depends=('libgit2.so')
makedepends=("cargo" "pandoc")
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/eza-community/eza/archive/v${pkgver}.tar.gz")
sha256sums=('78f56a35fc6707297f422647988b963f39bcef023bf55f6f2f5e7cd4be659a2a')
b2sums=('973ba81af8db663673a0b62d67bec4078886156303ecbd2315a03399c0eee9db79d0e2cf216bc479467e672dbe1bc5559b753b5564967e6b6bfd4e4a689a05d1')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname}-${pkgver}"
  cargo build --frozen --release
  mkdir -p target/man
  for manpage in eza.1 eza_colors.5 eza_colors-explanation.5; do
    pandoc --standalone -f markdown -t man "man/${manpage}.md" > "target/man/${manpage}"
  done
}

check() {
  cd "${pkgname}-${pkgver}"
  cargo test --frozen
  target/release/eza -la
}


package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  ln -s eza "${pkgdir}/usr/bin/exa"

  # install completions
  install -Dm644 "completions/bash/${pkgname}" -t "${pkgdir}/usr/share/bash-completion/completions"
  install -Dm644 "completions/zsh/_${pkgname}" -t "${pkgdir}/usr/share/zsh/site-functions/"
  install -Dm644 "completions/fish/${pkgname}.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"

  # install man pages
  install -Dm644 target/man/*.1 -t "${pkgdir}/usr/share/man/man1"
  install -Dm644 target/man/*.5 -t "${pkgdir}/usr/share/man/man5"

  install -Dm644 LICEN?E "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: ts=2 sw=2 et:
