# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Igor Dyatlov <dyatlov.igor@protonmail.com>

pkgname=rnote
pkgver=0.9.0
pkgrel=1
pkgdesc="A simple drawing application to create handwritten notes"
arch=('x86_64')
url="https://github.com/flxzt/rnote"
license=('GPL3')
depends=('gtk4' 'glib2' 'libadwaita' 'poppler-glib' 'gstreamer' 'alsa-lib')
makedepends=('meson' 'cargo' 'cmake' 'clang' 'git')
#checkdepends=('appstream-glib')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('ae615f1dc49e4e366ae417fb6ef1546213f598272f65ea8dd197888356769c90c5b27707f7da8e169f01a5e605237a9670709d9052b55fbdacd416b5f4e05824')
options=('!lto')

build() {
  arch-meson "$pkgname-$pkgver" build
  meson compile -C build
}

#check() {
#  meson test -C build
#}

package() {
  meson install -C build --destdir "$pkgdir"
}

# vim: ts=2 sw=2 et:
