# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=gitu
pkgver=0.16.0
pkgrel=1
pkgdesc="A TUI Git client inspired by Magit"
arch=('x86_64')
url="https://github.com/altsem/gitu"
license=('MIT')
depends=('gcc-libs' 'libgit2')
makedepends=('cargo')
checkdepends=('git')
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('0cc8c195ce35fb83e1a5a4a43e75f1c852ffffe4f1e3eeb3971f2d5128a01691')

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
