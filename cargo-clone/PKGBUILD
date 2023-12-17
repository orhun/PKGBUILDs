# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Funami

pkgname=cargo-clone
pkgver=1.2.1
pkgrel=3
pkgdesc="A cargo subcommand to fetch the source code of a Rust crate"
arch=('x86_64')
url="https://github.com/JanLikar/cargo-clone"
license=('Apache' 'MIT')
depends=('libgit2' 'curl')
checkdepends=('cargo' 'git')
makedepends=('libssh2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('c82a54b7651419664e92c106e3eeacff5080cca10faed6bef5931129a7bde182')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  export LIBSSH2_SYS_USE_PKG_CONFIG=1
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
