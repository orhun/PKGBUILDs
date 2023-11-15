# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=mirro-rs
pkgver=0.2.1
pkgrel=1
pkgdesc="An Arch Linux mirrorlist manager with a TUI"
arch=('x86_64')
url="https://github.com/rtkay123/mirro-rs"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('820cf0be8c270f42d40e4b844e02c8ca19b61bdf989ce4a95809d7db5f007a76b847416489436363fa0079f0075b2028e5f6eb2fd926bdf43b216786eb162975')
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
