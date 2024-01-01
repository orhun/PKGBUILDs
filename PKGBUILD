# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tui-journal
_pkgname=tjournal
pkgver=0.6.1
pkgrel=1
pkgdesc="Write and manage journals/notes from the terminal"
arch=('x86_64')
url="https://github.com/AmmarAbouZor/tui-journal"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('411c029cdd27de4af215d22d3879fe8f981a8905dd6ca594ae093edd792756919d810db1bd92954105a4f86934db518c85f805657390826d142e67492db5b73b')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
