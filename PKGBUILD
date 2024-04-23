# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=atac
pkgver=0.14.0
pkgrel=1
pkgdesc="A simple API client (postman like) in your terminal"
arch=('x86_64')
url="https://github.com/Julien-cpsn/ATAC"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('82b6e04965e901d2b635bccbbb9d2a42ef04c777dfe8b79174b5cee47d30986cef2b26c1b1959783874d994703724f303a2f890675ac68ae6ecd2862d8938ca7')
options=('!lto')

prepare() {
  cd "${pkgname^^}-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname^^}-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "${pkgname^^}-$pkgver"
  cargo test --frozen
}

package() {
  cd "${pkgname^^}-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
