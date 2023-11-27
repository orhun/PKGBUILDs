# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=lucky-commit
_pkgname=lucky_commit
pkgver=2.2.2
pkgrel=1
pkgdesc="Customize your git commit hashes"
arch=('x86_64')
url="https://github.com/not-an-aardvark/lucky-commit"
license=('MIT')
depends=('gcc-libs' 'ocl-icd')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('cf382a760dd948d3cc4cef8901c97d2a8e3305e877d619cd38a9331bccfd924c6f57b294ab48c9b4cc30c6858898c1546f9aede681877ab256f9347d0e01001d')

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
  cargo test --frozen --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
