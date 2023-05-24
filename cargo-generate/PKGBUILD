# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp A. <flying-sheep@web.de>

pkgname=cargo-generate
pkgver=0.18.3
pkgrel=1
pkgdesc="Use pre-existing git repositories as templates"
arch=('x86_64')
url="https://github.com/cargo-generate/cargo-generate"
license=('MIT' 'Apache')
depends=('curl' 'libgit2' 'libssh2' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('e44e021dbc83cc862e4f52fce76ed6cfab0cf08d74505fe177bec048f981ac9b')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo build --release --frozen --no-default-features
}

check() {
  cd "$pkgname-$pkgver"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo test --frozen --lib --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
