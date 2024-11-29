# Maintainer: orhun <orhunparmaksiz@gmail.com>
# https://github.com/orhun/pkgbuilds
# Maintainer: Adam Perkowski <adas1per@protonmail.com>
# https://github.com/adamperkowski/pkgbuilds

pkgname=nvrs
pkgver=0.1.5
pkgrel=1
pkgdesc="Fast new version checker for software releases"
arch=('x86_64')
url="https://github.com/adamperkowski/nvrs"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('6079f3522067ea764950a8c5a52d5ad3ef1dccf599b9a9c07422ad33e01018571248637d8ee1f7392903b26fb47c7419981311c7feece3f8384cb5fa81b7f978')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

# tests may be failing due to
# https://github.com/adamperkowski/nvrs/issues/7

#check() {
#  cd "$pkgname-$pkgver"
#  cargo test --release --frozen --lib
#  cargo test --release --frozen --bin nvrs
#}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}
