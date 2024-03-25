# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=hawkeye
pkgver=5.2.1
pkgrel=1
pkgdesc="Simple license header checker and formatter"
arch=('x86_64')
url="https://github.com/korandoru/hawkeye"
license=('Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo-nightly')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('286af151aa69cfcf92074b3e84be12a7762987cf0629ece981efb86876e31ad0')

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
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
