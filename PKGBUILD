# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=systemctl-tui
pkgver=0.3.4
pkgrel=1
pkgdesc="A fast, simple TUI for interacting with systemd services and their logs"
arch=('x86_64')
url="https://github.com/rgwood/systemctl-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('d20712068b753ff2977d65c6d0aff2f8fb20043a2593618f38ff3aa6fd0685dd3407ca45b5e5e3663c2c3b3617d382f364ba8d2b8d423ad0022634347fcd1b6b')

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
