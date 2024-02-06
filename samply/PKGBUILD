# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Cosmic <CosmicHorrorDev@pm.me>

pkgname=samply
pkgver=0.11.0
pkgrel=3
pkgdesc="A command-line sampling profiler for macOS and Linux"
arch=('x86_64')
url="https://github.com/mstange/samply"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('4def63bab3ab11cd0b02a725ae0fd477ba1d0147d30218b023868a930889b9c21507284b5b5168a3b519a5194d9ee2436ed712aaf4fd6f0f8a91405afc6fc54f')
options=('!lto')

prepare() {
  mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver/$pkgname"
  cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')" # --locked
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
  cd "$pkgname-$pkgver/$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 ../LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
