# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tauri
_pkgname=tauri
pkgver=1.5.7
pkgrel=1
pkgdesc="Command line interface for building Tauri apps"
arch=('x86_64')
url="https://github.com/tauri-apps/tauri"
license=('MIT' 'Apache')
depends=('gcc-libs' 'openssl' 'bzip2' 'libcroco' 'libffi')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/tauri-cli-v$pkgver.tar.gz")
sha512sums=('04d80920cd60283e575babfb85fe3530ee69505b974f6c02a635a951868617096f78c7d86e48bf48c3ec5218ae4c5469cd648b938f7df3dcdf1081e211538d87')
options=('!lto')

prepare() {
  mv "$_pkgname-tauri-cli-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/tooling/cli"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p completions
}

build() {
  cd "$pkgname-$pkgver/tooling/cli"
  cargo build --release --frozen
  local _completion="target/release/$pkgname completions --shell"
  # $_completion bash > "completions/$pkgname"
  $_completion fish > "completions/$pkgname.fish"
  $_completion zsh  > "completions/_$pkgname"
}

check() {
  cd "$pkgname-$pkgver/tooling/cli"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver/tooling/cli"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE_MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  # install -Dm664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
