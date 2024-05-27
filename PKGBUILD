# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyle Manna <kyle [at] kylemanna [dot] com>

pkgname=lurk
pkgver=0.3.5
pkgrel=1
pkgdesc="A pretty (simple) alternative to strace"
arch=('x86_64')
url="https://github.com/JakWai01/lurk"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('8d74eca342a61f7a020cc85253e5afc70a81c46c4936b927fd3158c65299a3b1f673a213274cc7d179caf27d0d74fa0a222459beabe4975dc85ad5fbd8c79bac')

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
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
