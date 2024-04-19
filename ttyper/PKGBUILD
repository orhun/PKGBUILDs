# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Adrian Groh <adrian[dot]groh[at]t[dash]online[dot]de>
# Contributor: Max Niederman <max@maxniederman.com>

pkgname=ttyper
pkgver=1.5.0
pkgrel=1
pkgdesc="Terminal-based typing test"
arch=('x86_64')
url="https://github.com/max-niederman/ttyper"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('ee21ec8a5d6c9b0d066d881de8f1170ad7a57a12329b66da51283f68a24002309d846e7206170e7d85cce3078c12bc425b656dae7f0043b8141e16e3b4c96931')

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
  install -Dm 644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
