# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Relwi <theofficialdork@hotmail.com>

pkgname=twitch-tui
_pkgname=twt
pkgver=2.6.6
pkgrel=2
pkgdesc="Twitch chat in the terminal"
arch=('x86_64')
url="https://github.com/Xithrius/twitch-tui"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('1eb9824aaebf7eedc31872b47abc700ef9449147137cf7e57a0142945011c87ab1568d081c2678999c88fe75ab76a697fb41c014aa5ac16f19468bbe791fcbce')
options=('!lto')

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
  install -Dm 644 LICENSE-MIT "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
