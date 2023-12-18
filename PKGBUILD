# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-depgraph
pkgver=1.6.0
pkgrel=2
pkgdesc="Creates dependency graphs for cargo projects using cargo metadata and graphviz"
arch=('x86_64')
url="https://github.com/jplatte/cargo-depgraph"
license=('GPL3')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver-lockfile.patch::$url/commit/a66ac0aa6741aaf58424161dbb5e6117c026872e.patch")
sha256sums=('d447316253217e0157af027c50bca10e84eba9f27b4f7c9642bcf38ad36d4766'
            '26400accd08e0d9b579f1f1f9d3d10048d55d3c0e2965f03403ce0aeca1a7f03')

prepare() {
  cd "$pkgname-$pkgver"
  patch -Np1 -i "$srcdir/$pkgname-$pkgver-lockfile.patch"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
}

# vim:set ts=2 sw=2 et:
