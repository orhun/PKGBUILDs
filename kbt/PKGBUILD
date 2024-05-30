# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Energi <bloznelis05@gmail.com>

pkgname=kbt
pkgver=2.1.0
pkgrel=1
pkgdesc="Keyboard tester in terminal"
arch=('x86_64')
url="https://github.com/bloznelis/kbt"
license=('MIT')
depends=('gcc-libs' 'libx11')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('d15b175653fb930e36c5ec3861fb76e9ca1fa728cbd4c02fc78498cddbf6bd499247dcf7ab11b10fcf746ba2ae20d63e379ea9bb86429641e131724836a0a467')

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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
