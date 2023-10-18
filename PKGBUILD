# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.12
_commit=2e5813b1ae0788ab26f3d7a31257fab35b54075a
pkgrel=1
pkgdesc="A cargo subcommand to provide various options useful for testing and CI"
arch=('x86_64')
url="https://github.com/taiki-e/cargo-hack"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo' 'git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "Cargo.lock")
sha512sums=('SKIP'
            'bf605d95ac4397382c2223054a2e45225f4b5221f5d505df1fe5efd534e959ef7a10c23f5f4b89bf8d66e5c6540e4e295f76a6f3c9279af7827409e6e6327bb2')

prepare() {
  cd "$pkgname"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname"
  cargo build --release --frozen
}

check() {
  cd "$pkgname"
  cargo test --frozen -- \
    --skip "multi_target" \
    --skip "version_range" \
    --skip "version_range_failure"
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
