# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-about
pkgver=0.6.1
pkgrel=1
pkgdesc="Cargo plugin to generate list of all licenses for a crate"
arch=('x86_64')
url="https://github.com/EmbarkStudios/cargo-about"
license=('Apache-2.0' 'MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('8ef8f0e2048b10fd2048db27c5400dd1d18be9e4a3a4735b4b7472debffecf38')
options=('!lto')

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
}

# vim:set ts=2 sw=2 et:
