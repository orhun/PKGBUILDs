# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp A. <flying-sheep@web.de>
# Contributor: Jian Zeng <anonymousknight96 AT gmail.com>

pkgname=cargo-expand
pkgver=1.0.59
pkgrel=1
pkgdesc="Subcommand to show result of macro expansion"
arch=('x86_64')
url='https://github.com/dtolnay/cargo-expand'
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('a33dc1e575db071b72fc2a0a7b59df0429842d9a545061b54dce691f96639f58')
options=('!lto')

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
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
