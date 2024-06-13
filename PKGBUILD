# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Chris Hillenbrand <chillenb.lists@gmail.com>
# Contributor: Pig Monkey <pm@pig-monkey.com>
# Contributor: Jean Lucas <jean@4ray.co>

pkgname=monolith
pkgver=2.8.1
pkgrel=3
pkgdesc="CLI to save web pages as single HTML files"
arch=('x86_64')
url="https://github.com/Y2Z/monolith"
license=('CC0-1.0')
depends=('openssl' 'gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('16bc9010f6a425ffa6cc71e01ab72bb3c9029f736c30918bff70157115b3ae9c')

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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
