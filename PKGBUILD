# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Adrian Groh <adrian[dot]groh[at]t[dash]online[dot]de>
# Contributor: Max Niederman <max@maxniederman.com>

pkgname=ttyper
pkgver=1.4.1
pkgrel=2
pkgdesc="Terminal-based typing test"
arch=('x86_64')
url="https://github.com/max-niederman/ttyper"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('6a7354b9725d961e2ad2709fcbe110f0e4c712a3b6a688468420bb29f507dade0de4eace140deff0ff3eec62d239d3a9484be732a6f90d1ad9d5e7f07c39e401')

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
  install -Dm 644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
