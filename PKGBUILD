# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-ndk
pkgver=3.5.5
pkgrel=1
pkgdesc="Compile Rust projects against the Android NDK without hassle"
arch=('x86_64')
url="https://github.com/bbqsrc/cargo-ndk"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('8dbf714916039ee6c709c9abbc437addbd79af6851e96e2f069622dd957fe6f5')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  depends+=('rustup')
}

# vim:set ts=2 sw=2 et:
