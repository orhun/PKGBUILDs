# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Cosmic <CosmicHorrorDev@pm.me>

pkgname=samply
pkgver=0.12.0
pkgrel=1
pkgdesc="A command-line sampling profiler for macOS and Linux"
arch=('x86_64')
url="https://github.com/mstange/samply"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('72a1b7efaa0217e5af791364e7e042d51c8c58c3588fdf7a869e2fa05ed5945d772a70ea18d637c0afd29de3887cc3bd79bb786c7468215b5cc08e93fd29c921')
options=('!lto')

prepare() {
  mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/$pkgname"
  cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')" --locked
}

build() {
  cd "$pkgname-$pkgver/$pkgname"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver/$pkgname"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
