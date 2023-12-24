# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=gfold
_commit=f1c0887e52cba5c464dd1de0bff14c4ae4f5287f
pkgver=4.4.1
pkgrel=1
pkgdesc="A CLI tool to help keep track of Git repositories"
arch=('x86_64')
url="https://github.com/nickgerace/gfold"
license=('Apache')
depends=('libgit2')
makedepends=('cargo' 'git')
source=("$pkgname-$pkgver::git+$url.git#commit=$_commit")
sha512sums=('SKIP')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
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
}

# vim: ts=2 sw=2 et:
