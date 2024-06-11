# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=bore
pkgver=0.5.1
pkgrel=1
pkgdesc="A command line tool for making tunnels to localhost"
arch=('x86_64')
url="https://github.com/ekzhang/bore"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('9d6db9bc52b404373e3edf5eb04f182c1bb5e1831ebeb5d075c66717ba652ac34afb8213211754f81944e828a0affa9fa6a91bf337d0aacbcb051239f9663551')

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
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
