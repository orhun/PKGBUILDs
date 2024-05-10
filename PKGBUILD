# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=blendr
pkgver=1.3.3
pkgrel=1
pkgdesc="The hacker's BLE (bluetooth low energy) browser terminal app"
arch=('x86_64')
url="https://github.com/dmtrKovalenko/blendr"
license=('BSD-3-Clause')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('e6a582cd9e9492531fa2944f5efb932d2d4e812d4fefd7b19d6d941936054f46c679b4fd183b3c93b16060436515b15fb493656b9b91be16c39f63f93a97866b')
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
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
