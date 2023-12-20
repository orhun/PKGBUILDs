# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-semver-checks
pkgver=0.26.0
_commit=0d1e24f04b2522ea1d2167e98b0575f775f2aa7a
pkgrel=3
pkgdesc='Scan your Rust crate for semver violations'
url='https://github.com/obi1kenobi/cargo-semver-checks'
license=('Apache' 'MIT')
arch=('x86_64')
depends=('cargo' 'gcc-libs' 'glibc' 'openssl' 'zlib')
makedepends=('git' 'cmake')
source=(
  "$pkgname::git+$url.git#commit=$_commit"
)
sha512sums=('SKIP')
options=('!lto')

prepare() {
  cd "$pkgname"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname"
  cargo build --release --frozen
}


check() {
  cd "$pkgname"
  ./scripts/regenerate_test_rustdocs.sh
  cargo test --frozen
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
