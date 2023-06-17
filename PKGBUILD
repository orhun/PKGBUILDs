# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=halp
pkgver=0.1.7
pkgrel=1
pkgdesc="A CLI tool to get help with CLI tools"
arch=('x86_64')
url="https://github.com/orhun/halp"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('6f30e87464c85c6c1d25d9a8e45fba0b245acdb2deab076d8f5306ee8b396fd9b55725277ed889ff3a8574acd9b3c82d19c7ac61469d5eac84a91e3b477090bf')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir completions/
  mkdir man/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  OUT_DIR=completions/ "./target/release/$pkgname-completions"
  OUT_DIR=man/ "./target/release/$pkgname-mangen"
}

check() {
  cd "$pkgname-$pkgver"
  OUT_DIR=target cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
