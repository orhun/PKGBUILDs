# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=jwt-cli
pkgver=6.0.0
pkgrel=1
pkgdesc="A super fast CLI tool to decode and encode JWTs"
arch=('x86_64')
url="https://github.com/mike-engel/jwt-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('2d0b7dfd98bc16448d1bd67763d7deea4be6ad5069134deacf6a3dcd5c64cf88f7b01fe09bdb03fc80845889706e3e172755b054f349a4c0141adafcd4458943')
options=('!lto')

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
  install -Dm 755 "target/release/jwt" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
