# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-rdme
pkgver=1.4.3
pkgrel=1
pkgdesc="Cargo command to create the README.md from your crate's documentation"
arch=('x86_64')
url="https://github.com/orium/cargo-rdme"
license=('MPL-2.0')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('3514fd4aacf031d257ce2b2f3b66851c36bee5a8941bc8a2097ad5e2dda9d985')
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
