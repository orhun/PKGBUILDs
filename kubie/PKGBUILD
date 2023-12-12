# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=kubie
pkgver=0.23.0
pkgrel=1
pkgdesc="A more powerful alternative to kubectx and kubens"
arch=('x86_64')
url="https://github.com/sbstp/kubie"
license=('custom:zlib')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('c92ee1a0d3d224ea9289766752aeceb16b58165d20799ab18afa1b8b84fa366270cc56368d4392ba36c8a3a6eb2ac5c96b33e3861c3d5dc9ac83a4a246f9fdb8')
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
