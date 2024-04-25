# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp Wolfer <ph.wolfer@gmail.com>

pkgname=gifski
pkgver=1.32.0
pkgrel=1
pkgdesc='GIF encoder based on libimagequant (pngquant). Squeezes maximum possible quality from the awful GIF format.'
arch=('x86_64')
url='https://gif.ski'
license=('AGPL3')
depends=('ffmpeg')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ImageOptim/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('0088917b5080c31efe98c76193b119069c1eb8ac9d50e98b207371ed2e22a3a4203f6f2cfee4b885d99d7d85d1f0d247831002997aac4058e8eb70b647f82988')
options=('!lto')

prepare() {
  cd $pkgname-$pkgver

  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}


build() {
  cd $pkgname-$pkgver

  cargo build --frozen --release --features=video
}

check() {
  cd $pkgname-$pkgver

  cargo test --frozen
}

package() {
  cd $pkgname-$pkgver

  install -Dm 755 target/release/gifski "$pkgdir"/usr/bin/gifski
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}
