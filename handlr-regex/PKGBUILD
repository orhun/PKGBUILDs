# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: ftilde <ftilde at tamepointer dot tld for germany>

pkgname=handlr-regex
_pkgname=handlr
pkgver=0.11.0
pkgrel=1
pkgdesc="Powerful alternative to xdg-utils written in Rust"
arch=('x86_64')
url="https://github.com/Anomalocaridid/handlr-regex"
license=('MIT')
provides=('handlr')
replaces=('handlr')
conflicts=('handlr')
depends=('shared-mime-info')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('e3bff91f9ff1137e14a82fc2a675d25d9dfac7b28620ebedae45745b18fba5d75ff6e837d798da17e7d78312bf27673a1bce794d54bac188d29267d42604ae48')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "assets/completions/$_pkgname" -t "$pkgdir/usr/share/bash-completion/completions"
  install -Dm 644 "assets/completions/$_pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "assets/completions/_$_pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
}

# vim: ts=2 sw=2 et:
