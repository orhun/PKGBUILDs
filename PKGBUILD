# Maintainer: kpcyrd <kpcyrd[at]archlinux[dot]org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=eza
pkgver=0.18.19
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
sha256sums=('b721cea8d9f7da7a9e17298911632912606bc51a983a0c1fc52340dbc4dc6ffa')
b2sums=('5eaa049717c2fc0b52eea0bc99b53856852f3fb7d1307f71a3e917b36c3f3ec0d1485b8f4d630e84fd645670c9a1f25cf5133690e1361fd14740674e775e02ce')

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
