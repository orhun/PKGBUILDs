# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rhit
pkgver=2.0.1
pkgrel=1
pkgdesc="A nginx log explorer"
arch=('x86_64')
url="https://github.com/Canop/rhit"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('2bc59c7eb24e655eba71f4cc540823c00619eba0673dadd8133f84490642ad13f1123781aefbf5434409b0f1699a1203dcfa7521b83417e74d7978856b5ee8b2')

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

# vim: ts=2 sw=2 et:
