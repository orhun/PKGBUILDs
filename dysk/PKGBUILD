# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=dysk
pkgver=2.6.1
pkgrel=1
pkgdesc="Get information on your mounted filesystems"
arch=('x86_64')
url="https://github.com/Canop/dysk"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
replaces=('lfs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('0a08c2ec0da83f54c1c4a9f59d93183ac05bfbeba4d2fd0f6273e118c0e270588befb20d6d39648e3025d94a07c86664698f647624f05bbbcc5a0f2c857a8ad9')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
