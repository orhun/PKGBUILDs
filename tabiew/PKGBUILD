# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tabiew
pkgver=0.3.2
pkgrel=1
pkgdesc="A lightweight TUI to view and query CSV files"
arch=('x86_64')
url="https://github.com/shshemi/tabiew"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('34f2ca4c696640d5d68c89c9b49070608f9bd6b62f1fcf652f0c5237532df112181d396a170eb3ebe0d1dbf14aca8dafc904177c8bce9f69d2439398f74d49ab')

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
  install -Dm 755 "target/release/tw" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
