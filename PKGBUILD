# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=caligula
pkgver=0.4.4
pkgrel=1
pkgdesc="A user-friendly, lightweight TUI for disk imaging"
arch=('x86_64')
url="https://github.com/ifd3f/caligula"
license=('GPL-3.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('8734b66d9c738076053bf5a707a0811c593b0920e9b87e7be0a4172c77b43ccde7185f552c03726d03151dbb7e01011092eb00512db800a83cd40c3c1efef35d')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  RUSTFLAGS="--cfg tracing_unstable" cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  RUSTFLAGS="--cfg tracing_unstable" cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
