# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Pig Fang <g-plane@hotmail.com>
# Contributor: SandaruKasa <sandarukasa+aur@ya.ru>
# Contributor: Evine Deng <evinedeng@hotmail.com>

pkgname=yazi
pkgver=0.2.3
pkgrel=1
pkgdesc="Blazing fast terminal file manager written in Rust, based on async I/O"
url="https://github.com/sxyazi/yazi"
arch=("x86_64")
license=('MIT')
depends=('gcc-libs' 'ttf-nerd-fonts-symbols')
optdepends=(
	'jq: for JSON preview'
	'unarchiver: for archive preview'
	'ffmpegthumbnailer: for video thumbnails'
	'fd: for file searching'
	'ripgrep: for file content searching'
	'fzf: for directory jumping'
	'poppler: for PDF preview'
	'zoxide: for directory jumping'
)
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/sxyazi/$pkgname/archive/v$pkgver.tar.gz")
sha256sums=('61b6b0372360bbe2b720a75127bef9325b7d507d544235d6a548db01424553e9')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  YAZI_GEN_COMPLETIONS=true cargo build --release --frozen
}

check() {
  cd "$pkgname"-$pkgver
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENCE"
  install -Dm644 "README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"

  cd "$pkgname-config/completions"
  install -Dm644 "$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm644 "$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm644 "_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
