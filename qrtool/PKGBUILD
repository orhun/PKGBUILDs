# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=qrtool
pkgver=0.10.10
pkgrel=1
pkgdesc="An utility for encoding or decoding QR code"
arch=('x86_64')
url="https://github.com/sorairolake/qrtool"
license=('MIT' 'Apache-2.0' 'CC-BY-4.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('598b24348be61b4d8df0498355800bb0c9f181a1b946e87f2a63248ed09104d5d3ae6e05560ec0edce19c3b59dfcebfe1285fcb1a48643480d83e76170b46442')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local compgen="target/release/$pkgname --generate-completion"
  $compgen bash >"completions/$pkgbase"
  $compgen elvish >"completions/$pkgbase.elv"
  $compgen fish >"completions/$pkgbase.fish"
  $compgen zsh >"completions/_$pkgbase"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSES/MIT.txt -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 LICENSES/CC-BY-4.0.txt -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 "completions/$pkgbase" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm644 "completions/$pkgbase.elv" -t "$pkgdir/usr/share/elvish/lib/"
  install -Dm644 "completions/$pkgbase.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm644 "completions/_$pkgbase" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
