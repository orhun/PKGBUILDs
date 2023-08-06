# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=kubie
pkgver=0.21.2
pkgrel=1
pkgdesc="A more powerful alternative to kubectx and kubens"
arch=('x86_64')
url="https://github.com/sbstp/kubie"
license=('custom:zlib')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('a067f66756f3de831e979bdaf9af98e6492e180233097604584ef50acb701d451070b3f56b18e8ef6441eb8304f02f2f3e22a85f34bfb85cd7e6b6df3b287371')
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
