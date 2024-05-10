# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-kanban
pkgver=0.9.6
pkgrel=1
pkgdesc='A kanban board for the terminal'
arch=('x86_64')
url='https://github.com/yashs662/rust_kanban'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('1e337f88213066c970f87e0cd26a53c10d1fbbefcdf8f7867a9672bf29225ca108151f8c1b7702df45094b3dcab7b9442add507eb230d0850b5c191fa29301dd')

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
