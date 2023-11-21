# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sven-Hendrik Haase <svenstaro@gmail.com>

pkgname=hex
_pkgname=hx
pkgver=0.5.0
pkgrel=1
pkgdesc="Futuristic take on hexdump"
arch=('x86_64')
url="https://github.com/sitkevij/hex"
license=(MIT)
depends=('gcc-libs')
makedepends=('cargo')
source=($pkgname-$pkgver.tar.gz::https://github.com/sitkevij/hex/archive/v${pkgver}.tar.gz)
sha512sums=('f69f55a911a7417ac80b7e6a3d53efba5af9f086045547a7f8308692624a4757b9171f7cd8b815b15fe4461c9318df17185e0d423b9b8dde571088947fa8f8fd')

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
