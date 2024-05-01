# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=atac
pkgver=0.15.0
pkgrel=1
pkgdesc="A simple API client (postman like) in your terminal"
arch=('x86_64')
url="https://github.com/Julien-cpsn/ATAC"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('74b23b1835c2d0a4ee7325867e6844619902d0f3815a96389686034ab44076ac603103c6d2b733096ebaede9aa892e1b4c2409de6bca5e411158194e05716b66')
options=('!lto')

prepare() {
  cd "${pkgname^^}-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname^^}-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "${pkgname^^}-$pkgver"
  cargo test --frozen
}

package() {
  cd "${pkgname^^}-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
