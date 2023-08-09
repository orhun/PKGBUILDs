# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sanpi <sanpi+aur@homecomputing.fr>

pkgname=cargo-spellcheck
pkgver=0.13.0
pkgrel=1
pkgdesc="Checks all your documentation for spelling and grammar mistakes"
arch=('x86_64')
url="https://github.com/drahnr/cargo-spellcheck"
license=('MIT' 'Apache')
depends=('hunspell')
makedepends=('cargo' 'clang' 'hunspell-en_US')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('02bc29e05ee0e3057b63f9912230113eba437f0921ca86fcee4e7d52f8fc9951')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p completions
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local _completion="target/release/$pkgname completions"
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
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
