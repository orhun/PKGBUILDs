# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: ftilde <ftilde at tamepointer dot tld for germany>

pkgname=handlr-regex
_pkgname=handlr
pkgver=0.10.1
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
sha512sums=('ca383b367944fbc0129fd1a05dfa80fa2974fb03f6eb455c9481d56fa15d90731de49e652d4cf818fd03322eba865ab8e3084d3ac6fa720c7a7852c3064ef72a')

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
