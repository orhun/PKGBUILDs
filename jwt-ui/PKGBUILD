# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=jwt-ui
pkgver=1.1.0
pkgrel=1
pkgdesc="A command line UI for decoding/encoding JSON Web Tokens"
arch=('x86_64')
url="https://github.com/jwt-rs/jwt-ui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('2a63f633700df8dd9ea209dadbf4ab7b0c1c3e81dcf2e3975e78482176ee22e6c8ada45cf2097cbab29d9825c8804469ba12be6d1559ab6583863940933eb6ef')
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
  install -Dm 755 "target/release/jwtui" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
