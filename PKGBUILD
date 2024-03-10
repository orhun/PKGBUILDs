# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: mexus <gilaldpellaeon@gmail.com>

pkgname=dua-cli
pkgver=2.29.0
pkgrel=1
pkgdesc="A tool to conveniently learn about the disk usage of directories, fast!"
arch=('x86_64')
url="https://github.com/Byron/dua-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/Byron/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('257a839f43c4f9155b819e6a1c6e268513ef9c53a49731234d3344c130276c7e724cc32b3545342d36459d892459568c78444f826f805aa6f34cf78aa8c498b8')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo build --release --locked
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm 644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm 644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm 755 "target/release/dua" "$pkgdir/usr/bin/dua"
}
