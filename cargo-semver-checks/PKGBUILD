# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-semver-checks
pkgver=0.31.0
_commit=44d5e0b376c976455976dc6d54b5660c43d806a8
pkgrel=1
pkgdesc='Scan your Rust crate for semver violations'
url='https://github.com/obi1kenobi/cargo-semver-checks'
license=('Apache-2.0' 'MIT')
arch=('x86_64')
depends=('cargo' 'gcc-libs' 'glibc' 'openssl' 'zlib')
makedepends=('git' 'cmake')
source=(
  "$pkgname-$pkgver::git+$url.git#commit=$_commit"
)
sha512sums=('9d7cc964d3686db448707ad905b6add1feb8ed63a72e7f8dd2333feeb2d131393806bd45e819848cee2bb8f8c54693d54be0c402d1abdcaf841d31c195cafabb')
options=('!lto')

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
  ./scripts/regenerate_test_rustdocs.sh
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
