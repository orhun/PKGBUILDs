# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=cargo-deb
pkgver=2.0.4
pkgrel=1
pkgdesc="Cargo subcommand that generates Debian packages"
arch=('x86_64')
url="https://github.com/kornelski/cargo-deb"
license=('MIT')
depends=('cargo' 'xz')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('79b256f53df147f4e1bf57edeed98f4140b2cecde256ca6f08470afe8310b636')

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
  # https://github.com/kornelski/cargo-deb/issues/111
  cargo test --frozen -- \
    --skip "dependencies::resolve_test" \
    --skip "manifest::tests" \
    --skip "control::tests" \
    --skip "build_with_explicit_compress_type"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
