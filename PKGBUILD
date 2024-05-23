# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=presenterm
pkgver=0.7.0
pkgrel=1
pkgdesc="A markdown terminal slideshow tool"
arch=('x86_64')
url="https://github.com/mfontanini/presenterm"
license=('BSD-2-Clause')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('d8a8e8982b0b1a98af138475d8280ae941e9c51f138eb492c4cb5a0b6e94d667ef0026bbeef3630faa6574cdc064210275ef4665b2c4681987ba2cc5b3362aa4')
options=('!lto')

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
