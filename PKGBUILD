# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: CupricReki
# Contributor: feschber

pkgname=lan-mouse
pkgver=0.8.0
pkgrel=1
pkgdesc="Software KVM Switch / mouse & keyboard sharing software for Local Area Networks"
arch=('x86_64')
url="https://github.com/feschber/lan-mouse"
license=("GPL-3.0-only")
depends=('libadwaita' 'gtk4' 'libx11' 'libxtst' 'glib2' 'gcc-libs' 'hicolor-icon-theme')
makedepends=('cargo' 'desktop-file-utils')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('4ab961f5305827c5d5b4f998edc1977e1d7ec0be10fed8f061780ff857faf688')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release --all-features
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all-features
}

package() {
  cd "$pkgname-$pkgver"

  desktop-file-install -m 644 --dir "$pkgdir/usr/share/applications/" "de.feschber.LanMouse.desktop"

  install -Dm0644 -t "$pkgdir/usr/share/icons/hicolor/scalable/apps" "resources/de.feschber.LanMouse.svg"
  install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
}

# vim: ts=2 sw=2 et:
