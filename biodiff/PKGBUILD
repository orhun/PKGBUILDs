# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: willemw <willemw12@gmail.com>
# Contributor: Daniel Maslowski <info@orangecms.org>

pkgname=biodiff
pkgver=1.1.0
pkgrel=3
pkgdesc='Hex diff viewer using alignment algorithms from biology'
arch=('x86_64')
url=https://github.com/8051Enthusiast/biodiff
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('f7960914ccf9b5fbdf3188b187d0cd3bca00f211487aa01d7b6f580da1c32312')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions
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
