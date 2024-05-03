# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=bugstalker
_pkgname=BugStalker
pkgver=0.1.5
pkgrel=1
pkgdesc="Rust debugger for Linux x86-64"
arch=('x86_64')
url="https://github.com/godzie44/BugStalker"
license=('MIT')
depends=('gcc-libs' 'libunwind')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('489930dfb3640906867479daa3013e299507eb86d683080e7471b1b97d85ecfaf1bb6a47d4f16744ad3224c25a35e20263ba654dd68ac9a54988917c50f07a61')
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
