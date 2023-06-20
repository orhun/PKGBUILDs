# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Julien Nicoulaud <julien.nicoulaud@gmail.com>

pkgname=zellij
pkgver=0.37.2
pkgrel=1
pkgdesc="A terminal multiplexer"
arch=('x86_64')
url="https://zellij.dev"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'mandown')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/zellij-org/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('6fd36a95573f439b1469a16622b04b12ff253479b981d3e3903ac8e59f795c842fddf6c8a49863020e9371bcdf30428c723c4a8fea2b012a9d00f1ce99219958')
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
