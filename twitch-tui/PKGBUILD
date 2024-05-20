# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Relwi <theofficialdork@hotmail.com>

pkgname=twitch-tui
_pkgname=twt
pkgver=2.6.10
pkgrel=1
pkgdesc="Twitch chat in the terminal"
arch=('x86_64')
url="https://github.com/Xithrius/twitch-tui"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3da206f93bb98bd78c4885b323863f745d9d73ce0fc03b5b90c3d0b7c3154d3c49c5ba5c483672a834d6e49ceb7d5f6eba097f2af660909ca6d2680dbd1dc3d3')
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
