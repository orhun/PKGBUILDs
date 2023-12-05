# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.14
_commit=71bdd924c638fa1d56d05840ce42530355f4ca46
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
            'e7d3b8539fc04da2a15087f3cdc3b90aece8fcefe6f50af9062001fc43af412b2db8d147e5e0117f0f1bac3bbe508dfea0b3dec0d73074d2823cbaf6a694127a')

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
