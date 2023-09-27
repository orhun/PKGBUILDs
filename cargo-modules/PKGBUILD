# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=cargo-modules
pkgver=0.9.3
pkgrel=1
pkgdesc="A cargo plugin for showing an overview of a crate's modules"
arch=('x86_64')
url="https://github.com/regexident/cargo-modules"
license=('MPL2')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('a7bf566d0297801877dc70c6e02b9f1066909f4c3e37a4fb45b56fc5683901b7')

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
}

# vim:set ts=2 sw=2 et:
