# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: CosmicHorror <LovecraftianHorror@pm.me>

pkgname=cargo-auditable
pkgver=0.6.3
pkgrel=1
pkgdesc="A cargo-subcommand to make production Rust binaries auditable"
arch=('x86_64')
url="https://github.com/rust-secure-code/cargo-auditable"
license=('Apache-2.0' 'MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('38825b2b8a8695792aa97cc82da9862a2a06fc33f73879a7a45b695af0fb7b331bae3fdce685c76c20a6371243a6f0a172e90ba888f6f73fc9a05977bada6551')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo build --release --frozen --features wasm
}

check() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo test --frozen -- --skip "test_wasm"
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 "$pkgname/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
