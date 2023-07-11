# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=arch-repro-status
pkgver=1.3.10
pkgrel=1
pkgdesc="Check the reproducibility status of your Arch Linux packages"
arch=('x86_64')
url="https://gitlab.archlinux.org/archlinux/arch-repro-status"
license=('MIT')
depends=('pacman')
makedepends=('cargo')
groups=('archlinux-tools')
source=("$pkgname-$pkgver.tar.gz::$url/-/archive/v$pkgver/$pkgname-v$pkgver.tar.gz")
sha512sums=('0dac1c6a75cabd617b03b62274bd3293ece8b7933efb205a384ba6686b1887da6801b0bf9842b95e66d9865e6b4d29975957844a0cd51b4b24f11e2a70180f85')

prepare() {
  cd "$pkgname-v$pkgver"
  mkdir completions/
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-v$pkgver"
  cargo build --frozen --release
  OUT_DIR=completions/ ./target/release/$pkgname-completions
}

check() {
  cd "$pkgname-v$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-v$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
}
