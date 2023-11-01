# Maintainer : Felix Yan <felixonmars@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rust-bindgen
_pkgname=bindgen
pkgver=0.69.0
pkgrel=1
pkgdesc='Automatically generates Rust FFI bindings to C (and some C++) libraries'
url='https://github.com/rust-lang/rust-bindgen'
depends=('gcc-libs' 'clang')
makedepends=('cargo')
arch=('x86_64')
license=('BSD')
source=("$pkgname-$pkgver.tar.gz::https://github.com/rust-lang/rust-bindgen/archive/v$pkgver.tar.gz")
sha512sums=('4ec403283cf26e09fb46182b35e2690bec7085bafb2469b4c3222c7b487eacf7000b4094acf8e85a98ae7c51988679f965359cae7abe07ef0ee6f5d9238ad8cc')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p completions
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
  # https://github.com/rust-lang/rust-bindgen/issues/2677
  local _completion="target/release/$_pkgname --generate-shell-completions"
  $_completion bash "x" > "completions/$_pkgname"
  $_completion fish "x" > "completions/$_pkgname.fish"
  $_completion zsh  "x" > "completions/_$_pkgname"
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
