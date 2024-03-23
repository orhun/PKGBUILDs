# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Stephan Springer <buzo+arch@Lini.de>
# Contributor: Darren Wu <$(base64 --decode <<<'ZGFycmVuMTk5NzA4MTBAZ21haWwuY29tCg==')>
# Contributor: Tarn Burton <twburton at gmail dot com>

pkgname=pioneer
pkgver=20240314
pkgrel=1
pkgdesc="A game of lonely space adventure"
arch=('x86_64')
url="https://github.com/pioneerspacesim/pioneer"
license=('GPL3')
conflicts=('pioneer-bin' 'pioneer-git' 'fmt')
depends=(
  'assimp'
  'freetype2'
  'glew'
  'hicolor-icon-theme'
  'libsigc++'
  'libvorbis'
  'lua52'
  'mesa'
  'sdl2_image'
)
makedepends=('cmake' 'ninja')
source=("$pkgname-$pkgver.tar.gz::https://github.com/pioneerspacesim/pioneer/archive/$pkgver.tar.gz")
sha256sums=('9cd31abd3e4d90cb589ecd628118dfb76ad5e98638361da666d76539b3269c3f')

prepare() {
    cd "$pkgname-$pkgver"
    # fix version string, don't use the build date
    sed -i 's|PROJECT_VERSION "%Y%m%d"|PROJECT_VERSION "'$pkgver'"|' CMakeLists.txt
}

build() {
    cmake -S "$pkgname-$pkgver" -B build -G Ninja \
          -D CMAKE_INSTALL_PREFIX:PATH=/usr \
          -D PIONEER_DATA_DIR:PATH=/usr/share/pioneer/data \
          -D USE_SYSTEM_LIBGLEW:BOOL=ON \
          -D USE_SYSTEM_LIBLUA:BOOL=ON \
          -D CMAKE_EXPORT_COMPILE_COMMANDS=1 \
          -Wno-dev

    cmake --build build --target all build-data
}

package() {
    DESTDIR="$pkgdir" cmake --install build

    # remove empty directories
    rmdir "$pkgdir"/usr/share/pioneer/data/music/core/{{un,}docked,near-planet}
}

# vim: ts=2 sw=2 et:
