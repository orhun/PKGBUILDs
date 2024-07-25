# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-semver-checks
pkgver=0.33.0
_commit=c112aa29b5cdc6535f0b4bd1b7669babcdbd9ae8
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
sha512sums=('9171b8aa5f3b5114f7bb663f85617c9ec059ec65d9df29267572ea4843f9e0b3553a9faf96aa8d41aa57e65504439fb5ebdb41824635c5c29c057a85cd9cf278')
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
