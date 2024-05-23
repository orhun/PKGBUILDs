# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=jwt-ui
pkgver=1.2.0
pkgrel=1
pkgdesc="A command line UI for decoding/encoding JSON Web Tokens"
arch=('x86_64')
url="https://github.com/jwt-rs/jwt-ui"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('ab7d35085fc6fc33558fd73b2081cda5740f992b93ee0db32f793a59d5895b9f9c07775b7f3f7931099de631cb4351614d605a1d45f7b159a427c449dace02e4')
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
  install -Dm 755 "target/release/jwtui" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
