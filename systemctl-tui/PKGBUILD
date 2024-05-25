# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=systemctl-tui
pkgver=0.3.6
pkgrel=1
pkgdesc="A fast, simple TUI for interacting with systemd services and their logs"
arch=('x86_64')
url="https://github.com/rgwood/systemctl-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('ac5951951ef41fc56ec96ecca06a894eed3e7e85ac0da3b9198ec4d77751789407627e47c92b06703fda657e2df058d456fa7dfb5160ca87453a47e0ede79266')

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
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
