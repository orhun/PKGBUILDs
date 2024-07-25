# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=atac
pkgver=0.16.0
pkgrel=1
pkgdesc="A simple API client (postman like) in your terminal"
arch=('x86_64')
url="https://github.com/Julien-cpsn/ATAC"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('a54fb009b0a901103acd9a0a4de3e82d0fc4508e5a2a2bd24749020c748ae206276e53adad2ec430518ca3b33abeafd80b6425c7db7b308937ddf5c41d1dc78b')
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
