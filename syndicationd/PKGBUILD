# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=syndicationd
_pkgname=synd-term
pkgver=0.1.10
pkgrel=1
pkgdesc="A TUI feed viewer"
arch=('x86_64')
url="https://github.com/ymgyt/syndicationd"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$_pkgname-v$pkgver.tar.gz")
sha256sums=('fa303484e0f4aab1c6d09faa88119c05c6331e3f5df8c3fc9ed4264f1a776758')
options=('!lto')

prepare() {
  cd "$pkgname-$_pkgname-v$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$_pkgname-v$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$_pkgname-v$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$_pkgname-v$pkgver"
  install -Dm 755 "target/release/synd" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
