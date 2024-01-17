# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tui-journal
_pkgname=tjournal
pkgver=0.8.0
pkgrel=1
pkgdesc="Write and manage journals/notes from the terminal"
arch=('x86_64')
url="https://github.com/AmmarAbouZor/tui-journal"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('ce29d19011186208287417c8a5ee0cb69a525f6e18fb785506eaf2ad3b7dcf1d5c2159635e2734b0739d7cf20e065b7398e7a45a098e36a45b95cd5feef21be9')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
