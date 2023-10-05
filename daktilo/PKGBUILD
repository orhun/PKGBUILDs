# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=daktilo
pkgver=0.2.1
pkgrel=1
pkgdesc="Turn your keyboard into a typewriter"
arch=('x86_64')
url="https://github.com/orhun/daktilo"
license=('MIT' 'Apache')
depends=('gcc-libs' 'alsa-lib' 'libxtst' 'libxi')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('472ef6d37ca6579ffe32f5c641402945dd26fe20e414b391e59ef4ab998882c1836c6d45dde0fa9e9b4ad064ede9ea0d96f456de3b6787d7a06c2f6329f125c5')

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
