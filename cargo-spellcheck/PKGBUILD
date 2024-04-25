# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sanpi <sanpi+aur@homecomputing.fr>

pkgname=cargo-spellcheck
pkgver=0.14.0
pkgrel=1
pkgdesc="Checks all your documentation for spelling and grammar mistakes"
arch=('x86_64')
url="https://github.com/drahnr/cargo-spellcheck"
license=('MIT' 'Apache-2.0')
depends=('cargo' 'hunspell')
makedepends=('clang' 'hunspell-en_US')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('1c3a80ab9cf604f605f4e3fb304acc529f68367edef7f0d041a871c371f6ebdd')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
