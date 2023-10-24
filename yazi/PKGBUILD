# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Pig Fang <g-plane@hotmail.com>
# Contributor: SandaruKasa <sandarukasa+aur@ya.ru>

pkgname=yazi
pkgver=0.1.5
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
sha256sums=('cfaf32fe58f68b7532f33b2a60e9507939ee54e32164db051357e059c553afec')
options=('!lto')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$srcdir/$pkgname"-$pkgver
  cargo test --frozen
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENCE"
  install -Dm644 "README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
  cd config
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
