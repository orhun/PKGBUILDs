# Maintainer : Felix Yan <felixonmars@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-bindgen
_pkgname=bindgen
pkgver=0.66.0
pkgrel=1
pkgdesc='Automatically generates Rust FFI bindings to C (and some C++) libraries'
url='https://github.com/rust-lang/rust-bindgen'
depends=('gcc-libs' 'clang')
makedepends=('cargo')
arch=('x86_64')
license=('BSD')
source=("$pkgname-$pkgver.tar.gz::https://github.com/rust-lang/rust-bindgen/archive/v$pkgver.tar.gz")
sha512sums=('5f14dbd89e915dc166cbaa6c947ac1b85fb8a1be20d1b69521c565d5b055ca3102cde8ecd59ac4886a62a41713e521d714f0030627e436e9ca4263e2eacbfcc2')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p completions
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
  local _completion="target/release/$_pkgname --generate-shell-completions"
  $_completion bash > "completions/$_pkgname"
  $_completion fish > "completions/$_pkgname.fish"
  $_completion zsh  > "completions/_$_pkgname"
}

package() {
  cd $pkgname-$pkgver
  install -Dm755 "target/release/$_pkgname" "$pkgdir"/usr/bin/bindgen
  install -Dm644 README.md "$pkgdir"/usr/share/doc/$pkgname/README.md
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  install -Dm664 "completions/$_pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm664 "completions/$_pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm664 "completions/_$_pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}
