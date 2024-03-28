# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=lucky-commit
_pkgname=lucky_commit
pkgver=2.2.3
pkgrel=1
pkgdesc="Customize your git commit hashes"
arch=('x86_64')
url="https://github.com/not-an-aardvark/lucky-commit"
license=('MIT')
depends=('gcc-libs' 'ocl-icd')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('299e66f404a742abed1d11ba104d3bda7c26c3b035c27c8a3e4beb28706a277d2408aae2e45034aa3cffb840e2d51af8dce61369c0164dee81fdc09f22422955')

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
  cargo test --frozen --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
