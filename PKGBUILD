# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-machete
pkgver=0.6.1
pkgrel=1
pkgdesc="Remove unused Rust dependencies"
arch=('x86_64')
url="https://github.com/bnjbvr/cargo-machete"
license=('MIT')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('1567ec91fe29ca96bef02f31ceacfa2ca084bd2e299cef486dc51cbdf79a1338')

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
 cargo test --release --locked
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
