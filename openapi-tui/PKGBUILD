# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=openapi-tui
pkgver=0.9.2
pkgrel=1
pkgdesc="Terminal UI to list, browse and run APIs defined with OpenAPI spec"
arch=('x86_64')
url="https://github.com/zaghaghi/openapi-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('ce35b3cb916261e8992f5051c531a5da891e280b884866effa58260a07e10c40')
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
