# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=kubie
pkgver=0.21.1
pkgrel=1
pkgdesc="A more powerful alternative to kubectx and kubens"
arch=('x86_64')
url="https://github.com/sbstp/kubie"
license=('custom:zlib')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('1398f0bf42cc2ea46844f2ec1a9a6a751a5d8817fca34f7d889a95c2449ad6ff24d7905c736abc348195e69f1377b1a833df8c3dfe83e57ad105ce031e07c5ce')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --no-default-features
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
  install -Dm 644 "completion/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completion/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
}

# vim: ts=2 sw=2 et:
