# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sven-Hendrik Haase <svenstaro@gmail.com>

pkgname=hex
_pkgname=hx
pkgver=0.6.0
pkgrel=1
pkgdesc="Futuristic take on hexdump"
arch=('x86_64')
url="https://github.com/sitkevij/hex"
license=(MIT)
depends=('gcc-libs')
makedepends=('cargo')
source=($pkgname-$pkgver.tar.gz::https://github.com/sitkevij/hex/archive/v${pkgver}.tar.gz)
sha512sums=('d5d787a34f1602c9ee1543844b59da83f81d70c1da16397b09ea96205e96f29fffd44a38d5a7f5655cf38626f3d3c73539afcde23d81e8f550758746f9dfc444')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

  cargo fetch --locked  
}

build() {
  cd "$srcdir/$pkgname-$pkgver"

  cargo build --release --frozen
}

check() {
  cd "$srcdir/$pkgname-$pkgver"

  cargo build --frozen
  cargo test --frozen
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  install -Dm755 "target/release/$_pkgname" "$pkgdir/usr/bin/$_pkgname"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  install -Dm644 README.md "$pkgdir"/usr/share/doc/$pkgname/README.md
  install -Dm644 "$_pkgname.1" "$pkgdir/usr/share/man/man1/$_pkgname.1"
}

# vim:set ts=2 sw=2 et:
