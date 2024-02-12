# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=cargo-deb
pkgver=2.0.6
pkgrel=1
pkgdesc="Cargo subcommand that generates Debian packages"
arch=('x86_64')
url="https://github.com/kornelski/cargo-deb"
license=('MIT')
depends=('cargo' 'xz')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('b8909878fa3c408719a2d8b0b80967c3340ef4201c52268ec8867a9349e83246')

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
