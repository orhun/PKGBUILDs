# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-kanban
pkgver=0.10.1
pkgrel=1
pkgdesc='A kanban board for the terminal'
arch=('x86_64')
url='https://github.com/yashs662/rust_kanban'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('2f9da5c89ed3d93c4d6c3bcc4fc2de26eae123aa27e359fed6f7ad5d537913740dbf34f512495cc3ee44cb006a27e8c9ccf7bb9e76977a334eed695506aff2e4')

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
