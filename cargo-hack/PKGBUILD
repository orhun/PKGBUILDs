# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.8
pkgrel=1
pkgdesc="A cargo subcommand to provide various options useful for testing and CI"
arch=('x86_64')
url="https://github.com/taiki-e/cargo-hack"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha512sums=('30f79dd1b76b7ce062fbc89dd8f0486d0beda59f1fb5b6b615858573782c129771824d16ec506d5d8911d16aaeb9c37d747c5c32de1ce094e5a84d6576175fa4'
            '1562f1ee9ec266ced92efe9e13a5212dc9862d4e892feb881cbedb203a28f126243fbae8ef91e0891049b43f1641472e167395d0b79d6ae77b85f09db7dc9ff8')

prepare() {
  cd "$pkgname-$pkgver"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- \
    --skip "multi_target" \
    --skip "version_range" \
    --skip "version_range_failure"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
