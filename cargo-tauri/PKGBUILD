# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tauri
_pkgname=tauri
pkgver=1.5.11
pkgrel=1
pkgdesc="Command line interface for building Tauri apps"
arch=('x86_64')
url="https://github.com/tauri-apps/tauri"
license=('MIT' 'Apache-2.0')
depends=('cargo' 'gcc-libs' 'openssl' 'bzip2' 'libcroco' 'libffi')
source=("$pkgname-$pkgver.tar.gz::$url/archive/tauri-cli-v$pkgver.tar.gz")
sha512sums=('5333eb2d0be492d4837e1d92715aafbaadc0480564a9568b0be28cb3fd60f498cea5517c0a604663e91edacaa6cfa57006466be4ef08a213039ed6cdece6e38d')
options=('!lto')

prepare() {
  mv "$_pkgname-tauri-cli-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/tooling/cli"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
