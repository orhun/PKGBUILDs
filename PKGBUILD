# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: CosmicHorror <LovecraftianHorror@pm.me>

pkgname=cargo-auditable
pkgver=0.6.2
pkgrel=1
pkgdesc="A cargo-subcommand to make production Rust binaries auditable"
arch=('x86_64')
url="https://github.com/rust-secure-code/cargo-auditable"
license=('Apache-2.0' 'MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('3656f124d8e43fbb4518d9aa3ad9e40a7cae61c56fa4718e9ff886934b2fcb5b2f116551c63ca17712c203ac93daf2b28a22efe41e556013189dec0ad9248f1f')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 "$pkgname/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
