# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: mexus <gilaldpellaeon@gmail.com>

pkgname=dua-cli
pkgver=2.27.1
pkgrel=1
pkgdesc="A tool to conveniently learn about the disk usage of directories, fast!"
arch=('x86_64')
url="https://github.com/Byron/dua-cli"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/Byron/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('7fa968757a1541ccb5d6e97ae7e3b9de96ed9779fbeeccd7848ae537cea32861f502dc3987e05c6109177b474803cfb8971616ffa83494986258ba8410f1852b')

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
