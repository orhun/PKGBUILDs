# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=qrtool
pkgver=0.11.3
pkgrel=1
pkgdesc="An utility for encoding or decoding QR code"
arch=('x86_64')
url="https://github.com/sorairolake/qrtool"
license=('MIT' 'Apache-2.0' 'CC-BY-4.0')
depends=('gcc-libs')
makedepends=('cargo' 'asciidoctor')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('91dcc214500ee64b36822c1c1b2c7bfdb1e9cad7e75c2c8e901cf733c85d11c596346487645998ad16113435e1a40447259066b3c550fc0013b9f685507ec219')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions/
  mkdir man/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local compgen="target/release/$pkgname --generate-completion"
  $compgen bash >"completions/$pkgbase"
  $compgen elvish >"completions/$pkgbase.elv"
  $compgen fish >"completions/$pkgbase.fish"
  $compgen zsh >"completions/_$pkgbase"
  asciidoctor -b manpage "docs/man/man1/$pkgname.1.adoc"
  asciidoctor -b manpage "docs/man/man1/$pkgname-encode.1.adoc"
  asciidoctor -b manpage "docs/man/man1/$pkgname-decode.1.adoc"
  asciidoctor -b manpage "docs/man/man1/$pkgname-help.1.adoc"
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
  install -Dm644 "docs/man/man1/$pkgname.1" -t "$pkgdir/usr/share/man/man1/"
  install -Dm644 "docs/man/man1/$pkgname-encode.1" -t "$pkgdir/usr/share/man/man1/"
  install -Dm644 "docs/man/man1/$pkgname-decode.1" -t "$pkgdir/usr/share/man/man1/"
  install -Dm644 "docs/man/man1/$pkgname-help.1" -t "$pkgdir/usr/share/man/man1/"
}

# vim: ts=2 sw=2 et:
