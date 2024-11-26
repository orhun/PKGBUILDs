# Maintainer: orhun <orhunparmaksiz@gmail.com>
# https://github.com/orhun/pkgbuilds
# Maintainer: Adam Perkowski <adas1per@protonmail.com>
# https://github.com/adamperkowski/pkgbuilds

pkgname=nvrs
pkgver=0.1.4
pkgrel=1
pkgdesc="Fast new version checker for software releases"
arch=('x86_64')
url="https://github.com/adamperkowski/nvrs"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('6dc9e105ee759cf6b7ecddb02a88c6dd535a05282a099ca876ab075cde09774eac8e3d5a5a08b549c20ca59db7a5b0d176b44c538cf2c45c1ade73a0e4c2cea5')

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
  cargo test --release --frozen --lib
  cargo test --release --frozen --bin nvrs
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}
