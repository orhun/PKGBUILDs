# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Dario Ostuni <dario.ostuni@gmail.com>

pkgname=wasm-pack
pkgver=0.12.0
pkgrel=1
pkgdesc="Your favorite rust -> wasm workflow tool!"
arch=('x86_64')
url="https://github.com/rustwasm/wasm-pack"
license=('MIT' 'Apache')
depends=('bzip2' 'curl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha384sums=('e0719cb83852c1917427f59494fd657579225e88212359602148cc1c5eb18ca2c652a4deb812ebb7ebadcdf6bae86d6a')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
