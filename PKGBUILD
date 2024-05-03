# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=systemctl-tui
pkgver=0.3.5
pkgrel=1
pkgdesc="A fast, simple TUI for interacting with systemd services and their logs"
arch=('x86_64')
url="https://github.com/rgwood/systemctl-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('0a6856fc99eb4a862623b1373984507559cf1010ec280b7ebe5248450a2afaf7b20d36d4cf8e79d03381e1700022794bb203808ee2c4e4df3acfb5b7e1c8165d')

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
