# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Pig Fang <g-plane@hotmail.com>
# Contributor: SandaruKasa <sandarukasa+aur@ya.ru>
# Contributor: Evine Deng <evinedeng@hotmail.com>

pkgname=yazi
pkgver=0.2.5
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
makedepends=('cargo' 'imagemagick')
source=("$pkgname-$pkgver.tar.gz::https://github.com/sxyazi/$pkgname/archive/v$pkgver.tar.gz")
sha256sums=('aea4a6ebd7f56c5d5fe6afbea143fc98c336d4ccd7852f2e8983c23e205988c4')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  VERGEN_GIT_SHA="Arch Linux" YAZI_GEN_COMPLETIONS=true cargo build --release --frozen
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
  install -Dm644 "assets/yazi.desktop" "$pkgdir/usr/share/applications/yazi.desktop"

  local r
  for r in 16 24 32 48 64 128 256; do
    install -dm755 "$pkgdir/usr/share/icons/hicolor/${r}x${r}/apps"
    convert assets/logo.png -resize "${r}x${r}" "$pkgdir/usr/share/icons/hicolor/${r}x${r}/apps/yazi.png"
  done

  cd "$pkgname-boot/completions"
  install -Dm644 "$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm644 "$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm644 "_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
