# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=chess-tui
pkgver=1.2.1
pkgrel=1
pkgdesc="Play chess in your terminal"
arch=('x86_64')
url="https://github.com/thomas-mauran/chess-tui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('c4de17ec56aeb4e513be382eb7d58899a75dc32faa51053aa32e7cdaf10f9e77cc7b97a18da1d256a9e5c81fdaf9c23ce26f480ef954da5f8c88c5bfe87686a8')

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
