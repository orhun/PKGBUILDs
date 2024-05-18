# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Relwi <theofficialdork@hotmail.com>

pkgname=twitch-tui
_pkgname=twt
pkgver=2.6.9
pkgrel=1
pkgdesc="Twitch chat in the terminal"
arch=('x86_64')
url="https://github.com/Xithrius/twitch-tui"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('92697a0848e000c8f128b0305eca2272f590170488b310b877868af45ba6541edef67dc186ae139437f6b831af2f4f8d0aa5899ca797572eaa085c9a675c19ac')
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
