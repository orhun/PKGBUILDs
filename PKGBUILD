# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-semver-checks
pkgver=0.32.0
_commit=1d74c88f48eaf15a1e2e492b79f8273bd15147f6
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
sha512sums=('4eaf58f58e121a847d2ec6426bac101f2cdcab2f97cfa7df22a654800f33ced7f5a33d5161e595e79fc3de8fe5e8e007f3b2aba3b0e1ea26d4ea4280e38d57af')
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
