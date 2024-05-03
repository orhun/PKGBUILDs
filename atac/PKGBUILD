# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=atac
pkgver=0.15.1
pkgrel=1
pkgdesc="A simple API client (postman like) in your terminal"
arch=('x86_64')
url="https://github.com/Julien-cpsn/ATAC"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('4564a7040482b54b7f2efddb86e5269dee501806c50d884cbbe8abf5a5b5f8380348fd9cd89c84943e13f9ec96b60b1ef5a6276c56ae6ea18c32c1c658376d0e')
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
