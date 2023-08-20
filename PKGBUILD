# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Alexander Bruegmann <mail[at]abruegmann[dot]eu>

pkgname=cargo-generate-rpm
pkgver=0.12.1
pkgrel=1
pkgdesc='Cargo helper command to generate a binary RPM package'
arch=('x86_64')
url="https://github.com/cat-in-136/cargo-generate-rpm"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('0e6e2093ec4d88ad373948b46f97633067a27c9eae2c6e0810b37a61b31c1a5e')
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
