# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=igrep
pkgver=1.2.0
pkgrel=1
pkgdesc="Interactive grep"
arch=('x86_64')
url="https://github.com/konradsz/igrep"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('ad488485a4dfa615733eee81d2ad6bd010e15b1a10031f906d64fb095be1ef017ed5cd44f5781f2ab5021fe892f80997211692845a9f89b8b689d5cc543428a2')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
  install -Dm 755 "target/release/ig" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
