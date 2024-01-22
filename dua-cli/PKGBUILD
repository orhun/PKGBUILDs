# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: mexus <gilaldpellaeon@gmail.com>

pkgname=dua-cli
pkgver=2.27.2
pkgrel=1
pkgdesc="A tool to conveniently learn about the disk usage of directories, fast!"
arch=('x86_64')
url="https://github.com/Byron/dua-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/Byron/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('44d89a53e62f97c6236851ebaf5628ceb97038a06485a118451987abb8f10c5362f5724f670d5bf5383378341d8e7e175a7c758c22b05ca44dd2154ef06b687b')

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
