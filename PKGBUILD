# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-rdme
pkgver=1.4.4
pkgrel=1
pkgdesc="Cargo command to create the README.md from your crate's documentation"
arch=('x86_64')
url="https://github.com/orium/cargo-rdme"
license=('MPL-2.0')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('631381a16eb23c7e2b0ae8c6a900f1f5c11d4329e9b6e901aaa15621ee2d274a')
options=('!lto')

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
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
