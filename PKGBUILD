# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=netscanner
pkgver=0.5.2
pkgrel=1
pkgdesc="Network scanner"
arch=('x86_64')
url="https://github.com/Chleba/netscanner"
license=('GPL3')
depends=('gcc-libs' 'iw')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f14cf5351e7fde2e2b604d71c844f35d986ab66796bcd53e978735f62fb7d96f5ee156693ff14cdd8d03f2d1da451cca73e1568a60d500d2b15dd53a04038f7d')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')" # --locked
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

# vim: ts=2 sw=2 et:
