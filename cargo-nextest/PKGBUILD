# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-nextest
pkgver=0.9.66
pkgrel=2
pkgdesc="A next-generation test runner for Rust."
arch=('x86_64')
url="https://github.com/nextest-rs/nextest"
license=('Apache' 'MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/cargo-nextest-$pkgver.tar.gz")
sha256sums=('2525fa66c6945821fc5b957b5cc41922c6879731bca8711f577f8794ef0b389d')
b2sums=('8e6a2a3c03af5bf62543d1e036c812a1c123c43c93e8fedba32adac8191c948469a3105583df29925612627dab3d18b57285d639c186974e46fdb923bebc2872')
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
