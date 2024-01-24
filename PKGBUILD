# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: mexus <gilaldpellaeon@gmail.com>

pkgname=dua-cli
pkgver=2.28.0
pkgrel=1
pkgdesc="A tool to conveniently learn about the disk usage of directories, fast!"
arch=('x86_64')
url="https://github.com/Byron/dua-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/Byron/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('b3bd4ec5a101a3e1e5a88d5de761f37a1ec1b71d6abe9d3aa1c72eac27ebfb19ce44365baec809c70cc9b77d295ca7e242554bf400a5460c45ab2b500f893da5')

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
