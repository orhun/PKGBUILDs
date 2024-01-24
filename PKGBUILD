# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp Wolfer <ph.wolfer@gmail.com>

pkgname=gifski
pkgver=1.14.1
pkgrel=1
pkgdesc='GIF encoder based on libimagequant (pngquant). Squeezes maximum possible quality from the awful GIF format.'
arch=('x86_64')
url='https://gif.ski'
license=('AGPL3')
depends=('ffmpeg')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ImageOptim/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('2155c9f1c202253d653934c5a028f718a494d1dd8c4bac44cef34797e4e355161aecfe1051b2fb49946ce8a96db409cc4dbf7cf10541f3eb15ab0078346d8680')
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
