# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=mirro-rs
pkgver=0.2.3
pkgrel=1
pkgdesc="An Arch Linux mirrorlist manager with a TUI"
arch=('x86_64')
url="https://github.com/rtkay123/mirro-rs"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('c2f8c790b4d827378e0642721bd69ee17ee57d60dedd3d583ccdc896658205505228b3a2755e5285b8260cb69e43ffc24efb8855de7b6cc47d959428404a174a')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
