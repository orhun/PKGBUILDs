# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-llvm-cov
pkgver=0.5.36
pkgrel=1
pkgdesc="Cargo subcommand to easily use LLVM source-based code coverage (-Z instrument-coverage)."
arch=('x86_64')
url="https://github.com/taiki-e/cargo-llvm-cov"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('60a910a235e1f509c03693a1f481c54c19901d3e059d24dc77fb51d08b649969'
            '9c7ad084d2321625a9c9d562d5811fdafcf3d542e62cefe303303b49b84fd911')

prepare() {
  cd "$pkgname-$pkgver"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
