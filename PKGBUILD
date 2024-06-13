# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=cargo-deb
pkgver=2.3.0
pkgrel=1
pkgdesc="Cargo subcommand that generates Debian packages"
arch=('x86_64')
url="https://github.com/kornelski/cargo-deb"
license=('MIT')
depends=('cargo' 'xz')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('61d92677e3951e391660b6825a8739d4d5c514e953053e2c354ce7dc04cae7a8')

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
    --skip "build_with_explicit_compress_type" \
    --skip "run_cargo_deb_command_on_example_dir_with_separate_debug_symbols"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
