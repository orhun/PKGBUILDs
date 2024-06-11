# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=tabiew
pkgver=0.3.5
pkgrel=1
pkgdesc="A lightweight TUI to view and query CSV files"
arch=('x86_64')
url="https://github.com/shshemi/tabiew"
license=('MIT')
depends=('gcc-libs' 'glibc')
makedepends=('cargo')
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('b6534077b8c1a10ea338361f40f9f0818f3a452843442540069a2721fee9dcf929751088bab85a28df1d918ad9a0b123ddffa678f17256bb6168968081026cc9')

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
  install -Dm 755 "target/release/tw" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
