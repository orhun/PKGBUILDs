# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rattler-build
pkgver=0.12.1
pkgrel=1
pkgdesc="A fast conda-package builder"
arch=('x86_64')
url="https://github.com/prefix-dev/rattler-build"
license=('BSD')
depends=('gcc-libs' 'openssl' 'bzip2' 'xz')
makedepends=('cargo')
checkdepends=('patchelf' 'git')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('a8672e6e32616f5380bdcb61d16f2d83d4b661d28453def99f01c47dd001258e2ead3124d421cdbe47c27dd1f3b7843aa21a41759ad8192d7adca57fc763d6fa')
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
