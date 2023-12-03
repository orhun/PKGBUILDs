# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-nextest
pkgver=0.9.64
pkgrel=1
pkgdesc="A next-generation test runner for Rust."
arch=('x86_64')
url="https://github.com/nextest-rs/nextest"
license=('Apache' 'MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/cargo-nextest-$pkgver.tar.gz")
sha256sums=('5617d471d9ce370cfa0d92ed59adfbbfea67f1ad272fee89f91c3a429c24a4ca')
b2sums=('a3d04c23812292ca5154c0d810e2e9a5135b71489c540339b4db14b0ffbb8056bc82b7634ee9151b1d407897c0a59d1b60546afd8de91b37e3225746e2c613c6')
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
