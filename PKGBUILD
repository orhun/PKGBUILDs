# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=eza
pkgver=0.11.1
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
sha256sums=('dbc2ee7c8c20383ab2ad5daeadd0ed4624ba41fea1791a6698ce1309bba1e27a')
b2sums=('e642be77d3402e4b42235cf13767fcef7279bc232c3e0b62bd012026293faae4a6dcaacf19f565f5f4f46f8e412d8f47921f8e1c8192f4bd642d17b1b91e950d')

prepare() {
  cd "${pkgname}-${pkgver}"
  sed -i 's/"vendored-libgit2"//' Cargo.toml
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
