# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

_pkgname=SongRec
pkgname=songrec
pkgver=0.4.1
pkgrel=1
pkgdesc='An open-source, unofficial Shazam client for Linux'
arch=('x86_64')
url='https://github.com/marin-m/SongRec'
license=('GPL3')
makedepends=('cargo' 'pkgconf' 'git')
depends=('gtk3' 'alsa-lib' 'openssl' 'ffmpeg')
optdepends=('libpulse: PulseAudio support')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('4f6fa72663adec8b1cb2bfd85d5807d1e1203a10c0f5774c50943837cc3c79ac')
options=('!lto')

prepare() {
  cd "$_pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$_pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$_pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$_pkgname-$pkgver"
  install -Dm 755 "target/release/songrec" "$pkgdir/usr/bin/songrec"

  install -Dm 644 "packaging/rootfs/usr/share/applications/com.github.marinm.songrec.desktop" \
                    "$pkgdir/usr/share/applications/com.github.marinm.songrec.desktop"

  install -Dm 644 "packaging/rootfs/usr/share/icons/hicolor/scalable/apps/com.github.marinm.songrec.svg" \
                    "$pkgdir/usr/share/icons/hicolor/scalable/apps/com.github.marinm.songrec.svg"

  install -Dm 644 "packaging/rootfs/usr/share/metainfo/com.github.marinm.songrec.metainfo.xml" \
                    "$pkgdir/usr/share/metainfo/com.github.marinm.songrec.metainfo.xml"

  mkdir -p "$pkgdir/usr/share/songrec"
  cp -ra "translations" "$pkgdir/usr/share/songrec/translations"

  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
