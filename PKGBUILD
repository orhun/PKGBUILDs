# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Adam Fontenot <adam.m.fontenot@gmail.com>
# Contributor: Daniel M. Capella <polyzen@archlinux.org>

pkgname=broot
pkgver=1.32.0
pkgrel=1
pkgdesc='Fuzzy Search + tree + cd'
arch=('x86_64')
url=https://github.com/Canop/broot
license=('MIT')
depends=('gcc-libs' 'zlib' 'libgit2' 'libxcb')
makedepends=('rust')
options=('!lto')
source=("https://github.com/Canop/broot/archive/v$pkgver/$pkgname-v$pkgver.tar.gz")
sha256sums=('0b9bf4a0dfa8a9cdcefcf18222dba4025379a8fa19190075835a99a507ae3d73')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen --features clipboard
}

check() {
  cd $pkgname-$pkgver
  cargo test --frozen
}

package() {
  cd $pkgname-$pkgver
  install -Dt "$pkgdir"/usr/bin target/release/$pkgname
  sed -i "s/#version/$pkgver/" man/page
  # Theoretically we could get the date from the CHANGELOG.md but it seems that the
  # CHANGELOG.md entry for the current version isn't actually in the current release.
  # changelog_date=$(sed -n "s/.*v$pkgver - \(.*\)$/\1/p" CHANGELOG.md)
  sed -i "s/#date//" man/page
  install -Dm644 man/page "$pkgdir/usr/share/man/man1/$pkgname.1"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 resources/icons/vscode/vscode.ttf "$pkgdir/usr/share/fonts/TTF/vscode.ttf"
}

# vim:set ts=2 sw=2 et:
