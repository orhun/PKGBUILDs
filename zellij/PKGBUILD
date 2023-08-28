# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien.nicoulaud@gmail.com>

pkgname=zellij
pkgver=0.38.0
pkgrel=1
pkgdesc="A terminal multiplexer"
arch=('x86_64')
url="https://zellij.dev"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'mandown')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/zellij-org/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('23792850ae7a4e50fce0e6ce0a901704c43501caceae8afe260bec0f777f0167746561d600a49876006d29d8b293aed91041ba667e272521fdbffe9636f915f5')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  RUSTUP_TOOLCHAIN=stable cargo build --release --frozen
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
}

# vim: ts=2 sw=2 et:
