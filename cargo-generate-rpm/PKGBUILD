# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Alexander Bruegmann <mail[at]abruegmann[dot]eu>

pkgname=cargo-generate-rpm
pkgver=0.11.0
pkgrel=1
pkgdesc='Cargo helper command to generate a binary RPM package'
arch=('x86_64')
url="https://github.com/cat-in-136/cargo-generate-rpm"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('c334f332214c5869754f0b2ce3e850a7a4f56cca68dbed5035e20d99b7acc885')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  # https://github.com/cat-in-136/cargo-generate-rpm/issues/60
  cargo fetch --target "$CARCH-unknown-linux-gnu" # --locked
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

# vim:set ts=2 sw=2 et:
