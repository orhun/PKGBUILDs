# Maintainer: orhun <orhunparmaksiz@gmail.com>
# https://github.com/orhun/pkgbuilds

pkgname=nvrs
pkgver=0.1.1
pkgrel=1
pkgdesc="Fast new version checker for software releases"
arch=('x86_64')
url="https://github.com/adamperkowski/nvrs"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f36cf5e11bb188bf8f1c0d3800b8d2ee2ac60b15e7ede0d0a2eb976005f2b656e1a21ac6747950d715f1fd2de9ae211856570b54392d668fbbc554070b3a79a1')

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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}
