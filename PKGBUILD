# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=caligula
pkgver=0.4.6
pkgrel=1
pkgdesc="A user-friendly, lightweight TUI for disk imaging"
arch=('x86_64')
url="https://github.com/ifd3f/caligula"
license=('GPL-3.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('41309639ea78d3377ae9b64dbefa34d482824e39f99afa9d9e63b123107fdf02384376314937466a02428d66cbd684914ffd7fc9c95c7c7cdf92e2f7b6c85fe6')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  RUSTFLAGS="--cfg tracing_unstable" cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  RUSTFLAGS="--cfg tracing_unstable" cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
