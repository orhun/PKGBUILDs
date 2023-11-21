# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=mirro-rs
pkgver=0.2.2
pkgrel=1
pkgdesc="An Arch Linux mirrorlist manager with a TUI"
arch=('x86_64')
url="https://github.com/rtkay123/mirro-rs"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('bcbfd6f75a7d7836715d02d6e35f83c0dbcc676ca4b6b00e529403d6f27968f7781a681c1e1dcd6d5d58d26619021c78f74651b741e85ed3f85458626e92ead5')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --features toml
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  out_dir=$(find target/release/build/ -wholename "*build/$pkgname*/out")
  install -Dm644 $out_dir/completions/$pkgname.bash "$pkgdir/usr/share/bash-completion/completions/$pkgname.bash"
  install -Dm644 $out_dir/completions/$pkgname.fish "$pkgdir/usr/share/fish/vendor_completions.d/$pkgname.fish"
  install -Dm644 $out_dir/completions/_$pkgname "$pkgdir/usr/share/zsh/site-functions/_$pkgname"
  install -Dm644 $out_dir/man/$pkgname.1 "$pkgdir/usr/share/man/man1/_$pkgname.1"
  install -Dm644 systemd/mirro-rs.service "$pkgdir/usr/lib/systemd/system/mirro-rs.service"
  install -Dm644 systemd/mirro-rs.timer "$pkgdir/usr/lib/systemd/system/mirro-rs.timer"
}

# vim: ts=2 sw=2 et:
