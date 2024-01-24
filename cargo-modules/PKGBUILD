# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=cargo-modules
pkgver=0.13.5
pkgrel=1
pkgdesc="A cargo plugin for showing an overview of a crate's modules"
arch=('x86_64')
url="https://github.com/regexident/cargo-modules"
license=('MPL2')
depends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('81067c7034255d8f3d697c78b68989fec82b558f85058d7e8633fbb10e7e4401')

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

# vim:set ts=2 sw=2 et:
