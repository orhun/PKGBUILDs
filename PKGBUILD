# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Relwi <theofficialdork@hotmail.com>

pkgname=twitch-tui
_pkgname=twt
pkgver=2.6.11
pkgrel=1
pkgdesc="Twitch chat in the terminal"
arch=('x86_64')
url="https://github.com/Xithrius/twitch-tui"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3e1c6f22c30ed95aad6cfdf4a1d095b24dbfb1209b2f9673ade7d908f49139c2d51354664efb49b3d91da0384bb0c15bfcbee2b9899f7fadd66ef97bb1c8a88d')
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
