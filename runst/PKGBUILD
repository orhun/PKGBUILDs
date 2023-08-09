# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=runst
pkgver=0.1.5
pkgrel=1
pkgdesc="A dead simple notification daemon"
arch=('x86_64')
url="https://github.com/orhun/runst"
license=('MIT' 'Apache')
depends=('dbus' 'pango')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('341a33c66d6b77dc660686283cdaf816fbbcf75c1a2cb661936d345d90b91e919ae8f91a6ba6fd17a7bf1053349c695c1514829015478d1cfbbe4dcccfb74a72')

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
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
