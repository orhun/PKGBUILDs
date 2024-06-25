# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=serpl
pkgver=0.1.26
pkgrel=1
pkgdesc="A simple TUI for search and replace, ala VS Code"
arch=('x86_64')
url="https://github.com/yassinebridi/serpl"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('c6047bcd39336fc6cf5b8d2e7f87cb855f612116deaa1c8d083a2d45cb8aa6c39e7c337378439e6151d0efa8643ecb3e1a2b11de8eba508d83d0735575bbfa10')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  VERGEN_GIT_DESCRIBE="Arch Linux" cargo build --release --frozen
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
