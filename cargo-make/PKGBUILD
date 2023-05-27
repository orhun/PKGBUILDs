# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>

pkgname=cargo-make
pkgver=0.36.8
pkgrel=1
pkgdesc='Rust task runner and build tool'
arch=('x86_64')
url='https://github.com/sagiegurari/cargo-make'
license=('Apache')
depends=('gcc-libs' 'openssl' 'bzip2')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('291067dd0420caf9c5c865217bf66971f773c230ee0814a58c4ee44277e13ce3')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"

  # download dependencies
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
