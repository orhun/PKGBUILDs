# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Igor Dyatlov <dyatlov.igor@protonmail.com>

pkgname=rnote
pkgver=0.10.0
pkgrel=1
pkgdesc="A simple drawing application to create handwritten notes"
arch=('x86_64')
url="https://github.com/flxzt/rnote"
license=('GPL3')
depends=('gtk4' 'glib2' 'libadwaita' 'poppler-glib' 'gstreamer' 'alsa-lib')
makedepends=('meson' 'cargo' 'cmake' 'clang' 'git')
#checkdepends=('appstream-glib')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('c14943157291efc5ad151ffa9e534d9aee3023f42451bf968a81e6009c13325d122d0a09245f33e139a74310e3ee75f5e019ab9ec129e9b8ac3d52c5b17280f2')
options=('!lto')

build() {
  arch-meson "$pkgname-$pkgver" build -Dcli=true
  meson compile -C build
}

#check() {
#  meson test -C build
#}

package() {
  meson install -C build --destdir "$pkgdir"
}

# vim: ts=2 sw=2 et:
