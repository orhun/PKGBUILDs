# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: wallace < str(11) + my_id at gmail dot com>
# Contributor: Iain Earl <iain at itmecho dot com>

pkgname=navi
pkgdesc="An interactive cheatsheet tool for the command-line"
pkgver=2.23.0
pkgrel=1
arch=('x86_64')
url='https://github.com/denisidoro/navi'
license=('Apache')
depends=('fzf')
optdepends=('skim: drop-in replacement for fzf')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('579a72814e7ba07dae697a58dc13b0f7d853532ec07229aff07a11e5828f3799')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir completions
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local _completion="target/release/$pkgname widget"
  $_completion bash > "completions/$pkgname"
  $_completion fish > "completions/$pkgname.fish"
  $_completion zsh  > "completions/_$pkgname"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  find docs -type f -exec install -Dm 644 -t "$pkgdir/usr/share/doc/$pkgname/" '{}' \;
  install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
