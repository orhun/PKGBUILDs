# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Julien Nicoulaud <julien.nicoulaud@gmail.com>

pkgname=zellij
pkgver=0.39.2
pkgrel=3
pkgdesc="A terminal multiplexer"
arch=('x86_64')
url="https://zellij.dev"
license=('MIT')
depends=(curl libcurl.so
         gcc-libs
         glibc)
makedepends=(cargo
             mandown)
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/zellij-org/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('4f77adfdad74fce1ece1abee6a354dc5fb2d81470ad798a76713b0c1c429d47d37f34a1e7c26949023c57d1ce57531f60df9f4bb1a5d5badd6fadcd62ffb4d30')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  ./target/release/zellij setup --generate-completion bash > target/zellij.bash
  ./target/release/zellij setup --generate-completion fish > target/zellij.fish
  ./target/release/zellij setup --generate-completion zsh > target/zellij.zsh
  mandown docs/MANPAGE.md > assets/zellij.1
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 target/release/zellij -t "${pkgdir}/usr/bin"
  install -Dm644 GOVERNANCE.md README.md -t "${pkgdir}/usr/share/doc/zellij"
  install -Dm644 LICENSE.md -t "${pkgdir}/usr/share/licenses/zellij"
  install -Dm644 target/zellij.bash "${pkgdir}/usr/share/bash-completion/completions/zellij"
  install -Dm644 target/zellij.fish "${pkgdir}/usr/share/fish/vendor_completions.d/zellij.fish"
  install -Dm644 target/zellij.zsh "${pkgdir}/usr/share/zsh/site-functions/_zellij"
  install -Dm644 assets/zellij.1 "${pkgdir}/usr/share/man/man1/zellij.1"
  install -Dm644 assets/zellij.desktop "${pkgdir}/usr/share/applications/zellij.desktop"
  install -Dm644 assets/logo.png "${pkgdir}/usr/share/pixmaps/zellij.png"
}

# vim: ts=2 sw=2 et:
