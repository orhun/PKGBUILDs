# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-nextest
pkgver=0.9.62
pkgrel=1
pkgdesc="A next-generation test runner for Rust."
arch=('x86_64')
url="https://github.com/nextest-rs/nextest"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/cargo-nextest-$pkgver.tar.gz")
sha256sums=('d3d412911da8701743a3f5833e8c188b5183cca3abadb2cb97d4eb28df9bfcf8')
b2sums=('a40482b2d2876c8a1314b085574053b042b421f2a76cbe89debf31852e58b8cc23e5ff9b0cd596be88730e6c97e409fa933e6cd686d56d7f374731aa5490109a')
options=('!lto')

prepare() {
  mv "nextest-$pkgname-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --package "$pkgname" --no-default-features --features default-no-update
}

check() {
  cd "$pkgname-$pkgver"
  cargo run --package cargo-nextest -- nextest run
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
