# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: İrem Ünlü < betulunlu0018 ~at~ gmail ~dot~ com >

pkgname=evcxr_repl
_pkgname=evcxr
pkgver=0.16.0
pkgrel=1
pkgdesc="A Rust REPL based on evcxr"
arch=('x86_64')
url="https://github.com/evcxr/evcxr"
license=('Apache')
depends=('gcc-libs' 'rust-src')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('ecd00c839a487cea5260bfc75c78ceba51e7215044b962081d7641c1292643bf')
options=('!lto')

prepare() {
  cd "$_pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$_pkgname-$pkgver"
  cargo build --release --frozen --package "$pkgname"
}

check() {
  cd "$_pkgname-$pkgver"
  cargo test --frozen --package "$pkgname"
}

package() {
  cd "$_pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
