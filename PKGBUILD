# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rattler-build
pkgver=0.18.0
pkgrel=1
pkgdesc="A fast conda-package builder"
arch=('x86_64')
url="https://github.com/prefix-dev/rattler-build"
license=('BSD')
depends=('gcc-libs' 'openssl' 'bzip2' 'xz')
makedepends=('cargo')
checkdepends=('patchelf' 'git')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('5b3a3adafde55b426c59e5e18999b91d286414a75a2e0b5fd5f96aeaf2656ee2e903b39c7f5e6802694318534d0336982b6259a6cca3b8f8b722f7dbf6c33470')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir -p completions/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  local _completion="target/release/$pkgname completion --shell"
  $_completion bash > "completions/$pkgbase"
  $_completion fish > "completions/$pkgbase.fish"
  $_completion zsh  > "completions/_$pkgbase"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- --skip "test_host_git_source"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
