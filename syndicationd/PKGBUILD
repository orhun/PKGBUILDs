# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=syndicationd
_pkgname=synd-term
pkgver=0.2.4
pkgrel=1
pkgdesc="A TUI feed viewer"
arch=('x86_64')
url="https://github.com/ymgyt/syndicationd"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$_pkgname-v$pkgver.tar.gz")
sha256sums=('a5348026678f1f27761d77130ef70b78a672f649d8a483a9a45865964aba1f0e')
options=('!lto')

prepare() {
  cd "$pkgname-$_pkgname-v$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$_pkgname-v$pkgver"
  RUSTFLAGS="--cfg tokio_unstable" cargo build --release --frozen
}

check() {
  cd "$pkgname-$_pkgname-v$pkgver"
  RUSTFLAGS="--cfg tokio_unstable" cargo test --frozen
}

package() {
  cd "$pkgname-$_pkgname-v$pkgver"
  install -Dm 755 "target/release/synd" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
