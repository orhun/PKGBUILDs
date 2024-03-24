# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-machete
pkgver=0.6.2
pkgrel=1
pkgdesc="Remove unused Rust dependencies"
arch=('x86_64')
url="https://github.com/bnjbvr/cargo-machete"
license=('MIT')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('21e22ec9d107fb14ae3ab76dc3c5ee0b233aa6f16a0946ee295b0bb5a712fffd')

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
