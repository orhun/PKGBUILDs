# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-binstall
pkgver=1.6.8
pkgrel=1
pkgdesc="Binary installation for Rust projects"
arch=('x86_64')
url="https://github.com/cargo-bins/cargo-binstall"
license=('GPL3')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('5641129239d1aca50e050ccd70d4712ab57e7cfe0d00882d7fc07ae52fdfa3bc')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
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
