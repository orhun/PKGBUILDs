# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=pixi
pkgver=0.21.0
pkgrel=1
pkgdesc="A package management and workflow tool"
arch=('x86_64')
url="https://github.com/prefix-dev/pixi"
license=('BSD-3-Clause')
depends=('gcc-libs' 'openssl' 'bzip2')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('c0ca407adba7eccea8d0ec6b5fb58f52b1b0be2db72234afcccf93f3c429a83ea194287e81659e0926e6ab8160e1ef3d3378410078cff4d9dee3b809f08349a1')
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
