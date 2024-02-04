# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.17
_commit=dbb5b75452caaa80ed83f71115fdbca706298271
pkgrel=1
pkgdesc="A cargo subcommand to provide various options useful for testing and CI"
arch=('x86_64')
url="https://github.com/taiki-e/cargo-hack"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo' 'git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "Cargo.lock")
sha512sums=('SKIP'
            '789e9926313dccc53034d5a845bbede1b119490ab04e63ab01f491c8cae9b1cc3372230e702943ee0018530c0b5683b9d2d1c7854b97dec43ca3eaa1758312ba')

prepare() {
  cd "$pkgname"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
  depends+=(rustup)
}

# vim: ts=2 sw=2 et:
