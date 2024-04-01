# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=openapi-tui
pkgver=0.7.1
pkgrel=1
pkgdesc="Terminal UI to list, browse and run APIs defined with OpenAPI spec"
arch=('x86_64')
url="https://github.com/zaghaghi/openapi-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('19f83492d9fa205fd1d7e8abb9fbc9d8ebf8504c05ff6e515a0033ec0b2e0d81')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  VERGEN_GIT_DESCRIBE="Arch Linux" cargo build --release --frozen
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

# vim: ts=2 sw=2 et:
