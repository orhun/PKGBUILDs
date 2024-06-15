# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=bugstalker
_pkgname=BugStalker
pkgver=0.2.1
pkgrel=1
pkgdesc="Rust debugger for Linux x86-64"
arch=('x86_64')
url="https://github.com/godzie44/BugStalker"
license=('MIT')
depends=('gcc-libs' 'libunwind')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('327a81e2211bb489f4aecce3e192ef3e152acaf71bd5f462552148fb46b4cf9accefe080a3e58b3336d2d4d44632201a6abd6dc814f88cf5a7958abf24d62fd7')
options=('!lto')

prepare() {
  mv "$_pkgname-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/bs" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
