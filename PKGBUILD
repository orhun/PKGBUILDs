# Maintainer: orhun <orhunparmaksiz@gmail.com>
# https://github.com/orhun/pkgbuilds
# Maintainer: Adam Perkowski <adas1per@protonmail.com>
# https://github.com/adamperkowski/pkgbuilds

pkgname=nvrs
pkgver=0.1.7
pkgrel=1
pkgdesc="Fast new version checker for software releases"
arch=('x86_64')
url="https://github.com/adamperkowski/nvrs"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('990747678c9ec3bc7b878bf201f47d938e1c5e0d387743810334ccc42c8c4f45b59ddcd610e8eeba41572040056c2f6f6d134a6d28e0bc843cec956792fb31fb')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  export CARGO_TARGET_DIR=target
  cargo build --release --frozen --bin "$pkgname" --features="${pkgname}_cli"
}

check() {
  cd "$pkgname-$pkgver"
  export CARGO_TARGET_DIR=target
  cargo test --frozen --features="${pkgname}_cli"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
