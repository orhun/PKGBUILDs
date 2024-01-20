# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=tui-journal
_pkgname=tjournal
pkgver=0.8.1
pkgrel=1
pkgdesc="Write and manage journals/notes from the terminal"
arch=('x86_64')
url="https://github.com/AmmarAbouZor/tui-journal"
license=('MIT')
depends=('gcc-libs' 'zlib')
makedepends=('cargo' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('7acf00418cb0a142596202c5e8bb46acaf4ba509a9b8d0ee590fd68860cf5d7645a20737504be1c43f589529a8e829f210e57ac6c1048f70ee27d75eaac0ea0a')
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
