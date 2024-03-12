# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: ftilde <ftilde at tamepointer dot tld for germany>

pkgname=handlr-regex
_pkgname=handlr
pkgver=0.9.0
pkgrel=2
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
sha512sums=('97bb63158bdafa1c904a698fce28be053620935a8fe4abb1385cd0a7e3aac64c80072489a35539c82b683ea73d90f132009a990e34f5158073d8b9e7341b4951')

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
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "assets/completions/$_pkgname" -t "$pkgdir/usr/share/bash-completion/completions"
  install -Dm 644 "assets/completions/$_pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "assets/completions/_$_pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
}

# vim: ts=2 sw=2 et:
