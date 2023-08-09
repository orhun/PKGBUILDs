# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=repgrep
_pkgname=rgr
pkgver=0.14.3
pkgrel=1
pkgdesc="An interactive command line replacer for ripgrep"
arch=('x86_64')
url="https://github.com/acheronfail/repgrep"
license=('MIT' 'Apache' 'Unlicense')
depends=('gcc-libs' 'ripgrep')
makedepends=('cargo' 'asciidoctor')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('15848e1db1ef4dbd46c1ae1ff1ce29b8bf13adffdd81e0b6648fe200dd6b22fe9e8fb9706770cae4639d2df76d8b0143c1ce79fd9e5565b9983b1b1371c234b9')

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
