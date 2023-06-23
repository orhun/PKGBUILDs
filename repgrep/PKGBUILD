# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=repgrep
_pkgname=rgr
pkgver=0.14.1
pkgrel=1
pkgdesc="An interactive command line replacer for ripgrep"
arch=('x86_64')
url="https://github.com/acheronfail/repgrep"
license=('MIT' 'Apache' 'Unlicense')
depends=('gcc-libs' 'ripgrep')
makedepends=('cargo' 'asciidoctor')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('20b68dd205c459eef917808c42ff82607693ecd21904c3ed865a79c884ad7b02bf38851bcb8d6f01bca2ea8a5b22d2741216939c70c31a0ea36dc2c745b54614')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  out_dir=$(find target -name repgrep-stamp -print0 | xargs -0 ls -t | head -n1 | xargs dirname)
  install -Dm 644 "$out_dir/$_pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$_pkgname"
  install -Dm 644 "$out_dir/$_pkgname.fish" "$pkgdir/usr/share/fish/vendor_completions.d/$_pkgname.fish"
  install -Dm 644 "$out_dir/_$_pkgname" "$pkgdir/usr/share/zsh/site-functions/_$_pkgname"
  install -Dm 644 "$out_dir/$_pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
