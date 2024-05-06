# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=havn
pkgver=0.1.11
pkgrel=1
pkgdesc="A fast configurable port scanner with reasonable defaults"
arch=('x86_64')
url="https://github.com/mrjackwills/havn"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('5106a4dabc34ae71bcd8739f86d6f20885204792c100be70035f785c6067e72e')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

# https://github.com/mrjackwills/havn/issues/2
# check() {
#   cd "$pkgname-$pkgver"
#   cargo test --frozen
# }

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
