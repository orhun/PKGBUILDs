# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=eza
pkgver=0.16.0
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
sha256sums=('611692d82618f29cfea3834fcd16a5b5e96bd14eefe0939180a2479892a88d09')
b2sums=('a70fd23fa3cef42cdcabc431677ba23dbbf23d8e1105224ef8d2c567bdaddf4cdc5acbb83554cfd34d0f4ae8e4d16ee6537bab3750c3a0a6246c923e5f7aac98')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
