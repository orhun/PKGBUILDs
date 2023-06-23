# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: KokaKiwi <kokakiwi+aur at kokakiwi dot net>

pkgname=cargo-semver-checks
pkgver=0.22.0
pkgrel=1
pkgdesc='Scan your Rust crate for semver violations'
url='https://github.com/obi1kenobi/cargo-semver-checks'
license=('Apache' 'MIT')
arch=('x86_64')
depends=('gcc-libs' 'glibc' 'libgit2' 'openssl' 'zlib')
makedepends=('cargo' 'git')
_commit=cbfbad811393bc8d04890d1d287926c90dc4eca0
source=(
  "$pkgname::git+$url.git#commit=$_commit"
  "$pkgname-0.21.0-downgrade_git2.patch"
)
sha512sums=('SKIP'
            '7bbbfaf1bc7eb1462a5ad6f8b955a90d57c5c2f1fd1cbb1e701b7b4225896f11d0afca6a03f75fdb038b474dd7508406c70600cfabff4b3b2cc2c126c9e1941e')
options=('!lto')

prepare() {
  cd "$pkgname"
  # downgrade git2 dependency, as it breaks index retrieval:
  # https://github.com/obi1kenobi/cargo-semver-checks/issues/468
  patch -Np1 -i ../"$pkgname-0.21.0-downgrade_git2.patch"
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
