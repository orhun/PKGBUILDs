# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=himalaya
pkgver=0.9.0
pkgrel=1
pkgdesc="A CLI email client"
arch=('x86_64')
url="https://github.com/soywod/himalaya"
license=('BSD')
depends=('gcc-libs' 'notmuch' 'openssl')
makedepends=('cargo')
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('0233289968a80672e39d7cd133f14bb9cd27129f389fccc4b366844389395a5bbfb89184e4d2b2ef2ecbbcaaf959a679f937f4b4b7c6018a52269a196c4af551')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p {completions,man}
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
  cargo build --frozen --release --features notmuch-backend
  local _completion="target/release/$pkgname completion"
  $_completion bash > "completions/$pkgname"
  $_completion fish > "completions/$pkgname.fish"
  $_completion zsh  > "completions/_$pkgname"
  local _mangen="target/release/$pkgname man"
  $_mangen man
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --features notmuch-backend -- --skip "test_imap_backend"
}

package_himalaya() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "assets/$pkgname.desktop" -t "$pkgdir/usr/share/applications"
  find man/ -type f -exec install -Dm 644 -t "$pkgdir/usr/share/man/man1" {} \;
}

# vim:set ts=2 sw=2 et:
