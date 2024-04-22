# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=bugstalker
_pkgname=BugStalker
pkgver=0.1.4
pkgrel=1
pkgdesc="Rust debugger for Linux x86-64"
arch=('x86_64')
url="https://github.com/godzie44/BugStalker"
license=('MIT')
depends=('gcc-libs' 'libunwind')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('b536b8ecd059ddd9c9fc486ccc1000274e6a4c619fda16ff0ca2f890a6dfb58920841b6a2c240648f4fd3e71e1e9362e3a7c78df11ed8e0974c68a08947fc2ed')
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
