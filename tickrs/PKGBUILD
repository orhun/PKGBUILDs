# Maintainer:  Orhun Parmaksız <orhun@archlinux.org>

pkgname=tickrs
epoch=2
pkgver=0.14.9
pkgrel=1
pkgdesc="Realtime ticker data in your terminal"
arch=('x86_64')
url="https://github.com/tarkah/tickrs"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('930a24f84abcf16ed019e5776a72b7021a5131c964733131851a747d7c669edec8ed8ee416a31d94b07cb05a319e4acfc5b64779e31a34811d0303ba391cb9ec')
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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}
