# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=eza
pkgver=0.18.17
pkgrel=1
pkgdesc="A modern replacement for ls (community fork of exa)"
url="https://github.com/eza-community/eza"
arch=(x86_64)
license=(MIT)
provides=(exa)
replaces=(exa)
conflicts=(exa)
depends=(gcc-libs # libgcc_s.so
         glibc # libc.so libm.so
         libgit2
         zlib)
makedepends=("cargo" "pandoc")
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('fb9eea00bff8ad0283c046398259f03b1ce2830a49cdd7417b65c9dade07d709')
b2sums=('6c4db0e88a65a58deaeba09e4350db39a468a5821e6d1ad70173d885f6525e8e88c01303ba2b6300660206e3b72b23ab5f416424f0dd3a01db0ef36f82630eb5')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname}-${pkgver}"
  CFLAGS+=' -ffat-lto-objects'
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
  depends+=(libgit2.so
            libz.so)
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
