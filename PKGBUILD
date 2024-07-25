# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=serpl
pkgver=0.3.1
pkgrel=1
pkgdesc="A simple TUI for search and replace, ala VS Code"
arch=('x86_64')
url="https://github.com/yassinebridi/serpl"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('7aa60e540033f33d5599b25fe860c770bf37f2cdbe55af12106f3702b61ec3f7c24e822c7d5a1e2b63edb858869d5a84d2ed20e8d4ccbab75a33debf2b37eb56')

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
