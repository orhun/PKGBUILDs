# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Alexander Bruegmann <mail[at]abruegmann[dot]eu>

pkgname=cargo-generate-rpm
pkgver=0.13.0
pkgrel=2
pkgdesc='Cargo helper command to generate a binary RPM package'
arch=('x86_64')
url="https://github.com/cat-in-136/cargo-generate-rpm"
license=('MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('fa27b584df345ea38b34894a2cd276e23ff3e82257f0509cb07c976faea4bedc')
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
