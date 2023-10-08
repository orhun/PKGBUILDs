# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tui-journal
_pkgname=tjournal
pkgver=0.3.3
pkgrel=1
pkgdesc="Write and manage journals/notes from the terminal"
arch=('x86_64')
url="https://github.com/AmmarAbouZor/tui-journal"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('608649b200a849ec6575664b13906a746c37bc32d25f43184cbf36b6aa4a4b975e4bd80f6a2cebb504eb5e9bcd86fcccaf729d4323584f95e9caf440de05aa17')
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
