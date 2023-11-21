# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Wesley Moore <wes@wezm.net>

pkgname=viu
pkgver=1.5.0
pkgrel=1
pkgdesc="Simple terminal image viewer"
arch=('x86_64')
url="https://github.com/atanunq/viu"
license=('MIT')
depends=('gcc-libs' 'libsixel')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('9682be1561f7a128436bd2e45d1f8f7146ca1dd7f528a69bd3c171e4e855474b')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release --features sixel
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
