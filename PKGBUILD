# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>

pkgname=cargo-make
pkgver=0.37.10
pkgrel=1
pkgdesc='Rust task runner and build tool'
arch=('x86_64')
url='https://github.com/sagiegurari/cargo-make'
license=('Apache-2.0')
depends=('cargo' 'gcc-libs' 'openssl' 'bzip2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('37038d998b19d3a798cf99ffdcc0decfd35929c3a46901b3de46f10c46bb831c')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"

  # download dependencies
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"

  cargo build --release --frozen
}

package() {
  cd "$pkgname-$pkgver"

  # binary
  install -vDm755 -t "$pkgdir/usr/bin" target/release/{cargo-make,makers}

  # license
  install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE

  # documentation
  install -vDm644 -t "$pkgdir/usr/share/doc/$pkgname" *.md

  # shell auto-completion
  install -vDm644 extra/shell/makers-completion.bash "$pkgdir/usr/share/bash-completion/completions/makers"
}

# vim:set ts=2 sw=2 et:
