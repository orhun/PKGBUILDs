# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tui-journal
_pkgname=tjournal
pkgver=0.6.0
pkgrel=1
pkgdesc="Write and manage journals/notes from the terminal"
arch=('x86_64')
url="https://github.com/AmmarAbouZor/tui-journal"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f81d8d47bbf6fc6a2fb6ed444fc43cffcb336e8fe61f9fbc67234f2705710add6c6222ba635be5d24c702e672986c0da65aa41755060b08c84e7e577c8ef9077')
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
