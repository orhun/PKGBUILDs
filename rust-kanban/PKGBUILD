# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-kanban
pkgver=0.9.7
pkgrel=1
pkgdesc='A kanban board for the terminal'
arch=('x86_64')
url='https://github.com/yashs662/rust_kanban'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('6a49935e6a6e1678443c1ec679747926bc93fd3a6bcc8acbf0d224942dd5acb4cf40977a2f6b8d417d756218208facbd46a1370c7d2e5f78b189370fc74bebd2')

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
