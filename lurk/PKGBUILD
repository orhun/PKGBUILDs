# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyle Manna <kyle [at] kylemanna [dot] com>

pkgname=lurk
pkgver=0.3.4
pkgrel=1
pkgdesc="A pretty (simple) alternative to strace"
arch=('x86_64')
url="https://github.com/JakWai01/lurk"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f545b83f5f6fc84399419394c606e3d7c9c4a5ed094ae171f4f226768609ee7c1d364d13f862efd6aa2d21615cd7c14165dc3c4c4a2b2f9148fba4963b62f401')

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

# vim: ts=2 sw=2 et:
