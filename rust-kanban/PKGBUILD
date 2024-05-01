# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-kanban
pkgver=0.9.5
pkgrel=1
pkgdesc='A kanban board for the terminal'
arch=('x86_64')
url='https://github.com/yashs662/rust_kanban'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3e8b8a3f68bcfaae0286c9bce88247e6cb57d1d77f832884ffc484c9bf55dcbf74a99b6a66b41d32493ef5d48b466c0984d5a04e6b2fa386cd2c4131d7b75e94')

prepare() {
  cd "${pkgname/-/_}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname/-/_}-${pkgver}"
  cargo build --release --frozen
}

check() {
  cd "${pkgname/-/_}-${pkgver}"
  cargo test --frozen
}

package() {
  cd "${pkgname/-/_}-${pkgver}"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
