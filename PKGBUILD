# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=pixi
pkgver=0.12.0
pkgrel=1
pkgdesc="A package management and workflow tool"
arch=('x86_64')
url="https://github.com/prefix-dev/pixi"
license=('BSD')
depends=('gcc-libs' 'openssl' 'bzip2')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('a92ac175058b42bb9628fd049fb05b88509b5d6807ca1686a297e385d40ac9cee37900638646e57546b5d630304758564ad8165785c0557d7ef334b1d467bd46')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir -p completions/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local _completion="target/release/$pkgname completion"
  $_completion --shell bash > "completions/$pkgbase"
  $_completion --shell fish > "completions/$pkgbase.fish"
  $_completion --shell zsh  > "completions/_$pkgbase"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
