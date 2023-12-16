# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-about
pkgver=0.6.0
pkgrel=2
pkgdesc="Cargo plugin to generate list of all licenses for a crate"
arch=('x86_64')
url="https://github.com/EmbarkStudios/cargo-about"
license=('Apache' 'MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('b2967f406d68cb09dff8ffea4f60c398ad873a41ac19e6a841e30e22c730791d')
options=('!lto')

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

# vim:set ts=2 sw=2 et:
