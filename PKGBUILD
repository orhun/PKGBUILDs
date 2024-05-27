# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=jwt-cli
_pkgname=jwt
pkgver=6.1.0
pkgrel=1
pkgdesc="A super fast CLI tool to decode and encode JWTs"
arch=('x86_64')
url="https://github.com/mike-engel/jwt-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('5a9622ad4a1a7b153b96a3b7390179496a084875ebb4e2400502e1351b6f218b879ea7e114f9a8953a4ea51b8047edb9ab56ce71910428f5256932cfb9878a41')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local compgen="target/release/$_pkgname completion"
  $compgen bash >"completions/$pkgname"
  $compgen elvish >"completions/$pkgname.elv"
  $compgen fish >"completions/$pkgname.fish"
  $compgen zsh >"completions/_$pkgname"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm644 "completions/$pkgname.elv" -t "$pkgdir/usr/share/elvish/lib/"
  install -Dm644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
