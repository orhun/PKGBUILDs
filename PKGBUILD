# Maintainer: Stephan Springer <buzo+arch@Lini.de>
# Contributor: Darren Wu <$(base64 --decode <<<'ZGFycmVuMTk5NzA4MTBAZ21haWwuY29tCg==')>
# Contributor: Tarn Burton <twburton at gmail dot com>

pkgname=pioneer
pkgver=20210203
pkgrel=2
pkgdesc="A game of lonely space adventure"
arch=('x86_64') # 'i686' untested
url="https://github.com/pioneerspacesim/pioneer"
license=('GPL3')
provides=('pioneer')
conflicts=('pioneer-bin' 'pioneer-git')
depends=(
  'assimp' # libassimp-dev >= 3.2
  'curl' # libcurl-dev
  'freetype2' # libfreetype6-dev
  'glew' # USE_SYSTEM_LIBGLEW include <GL/glew.h>
  'hicolor-icon-theme'
  'libpng' # libpng-dev
  'libsigc++' # libsigc++-dev libsigc++-2.0-dev
  'libvorbis' # libvorbis-dev
  'lua52' # USE_SYSTEM_LIBLUA
  'mesa' # mesa-common-dev
  'sdl2' # libsdl2-dev
  'sdl2_image' # libsdl2-image-dev
)
makedepends=(automake naturaldocs pkgconf cmake ninja)
source=("$pkgname-$pkgver.tar.gz::https://github.com/pioneerspacesim/pioneer/archive/$pkgver.tar.gz")
sha256sums=('fcbc57374123b44161e9d15d97bd950255f654a222840894f50bfc2be716ea68')

build()
{
    cmake -S "$pkgname-$pkgver" -B build -G Ninja \
          -D CMAKE_INSTALL_PREFIX:PATH=/usr \
          -D PIONEER_DATA_DIR:PATH=/usr/share/pioneer/ \
          -D USE_SYSTEM_LIBGLEW:BOOL=ON \
          -D USE_SYSTEM_LIBLUA:BOOL=ON \
          -D CMAKE_EXPORT_COMPILE_COMMANDS=1 \
          -Wno-dev

    cmake --build build --target all build-data codedoc
}

package()
{
    DESTDIR="$pkgdir" cmake --install build

    # appdata
    mv "$pkgdir"/usr/share/{appdata,metainfo}

    # remove empty directories
    rmdir "$pkgdir"/usr/share/pioneer/music/core/{{un,}docked,near-planet}

    # codedoc
    mkdir --parents "$pkgdir/usr/share/doc"
    cp --recursive "$pkgname-$pkgver"/codedoc "$pkgdir"/usr/share/doc/pioneer
}
