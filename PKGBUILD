# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=ripasso
pkgver=0.6.5
pkgrel=1
pkgdesc="A simple password manager written in Rust"
arch=('x86_64')
url="https://github.com/cortex/ripasso"
license=('GPL3')
depends=('openssl' 'libxcb' 'libgpg-error' 'zlib' 'gpgme' 'libgit2')
makedepends=('gettext' 'cargo' 'clang' 'python' 'gtk4' 'qt5-base')
source=("$pkgname-$pkgver.tar.gz::$url/archive/release-$pkgver.tar.gz")
sha512sums=('1b6990f96f2e6000530fc5cecdef513c5deb367146d886d41aacdd412c44de8754e6711df6f5535feefdacb6aad68520d6a55868d6f0ba5928412739dcf0bb3a')
options=('!lto')

prepare() {
  mv "$pkgname-release-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build -p "ripasso-cursive" --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm0755 "target/release/ripasso-cursive" "$pkgdir/usr/bin/$pkgname"
  install -Dm0644 "target/man-page/cursive/ripasso-cursive.1" "$pkgdir/usr/share/man/man1/$pkgname.1"
  install -Dm0644 README.md -t "$pkgdir/usr/share/doc/$pkgname"

  mkdir -p "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/de.mo" "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/fr.mo" "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/it.mo" "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/nb.mo" "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/nn.mo" "$pkgdir/usr/share/ripasso/"
  install -Dm0644 "target/translations/cursive/sv.mo" "$pkgdir/usr/share/ripasso/"
}

# vim: ts=2 sw=2 et:
