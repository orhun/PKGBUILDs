# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp Wolfer <ph.wolfer@gmail.com>

pkgname=gifski
pkgver=1.14.2
pkgrel=1
pkgdesc='GIF encoder based on libimagequant (pngquant). Squeezes maximum possible quality from the awful GIF format.'
arch=('x86_64')
url='https://gif.ski'
license=('AGPL3')
depends=('ffmpeg')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ImageOptim/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('6b0fea3e170d00af9febb5b761514b3ca4e8d46547134dfc7bcf524588cd16197b5ec8623d15147eaf2c5f120ffce585bb76947781ae69fb34a5c28d54dd3799')
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
