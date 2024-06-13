# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=sig
pkgver=0.1.2
pkgrel=1
pkgdesc="Interactive grep for streaming"
arch=('x86_64')
url="https://github.com/ynqa/sig"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3d7f0e1f46c4dd83c65ca65088cfc8f122ef32f37bc3b8bebedda9fb04ae1f73d83c0742e773bb66f1b331e4c3e3bbd7ecae61dd0465b60238a858aa266d7220')

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
