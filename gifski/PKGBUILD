# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp Wolfer <ph.wolfer@gmail.com>

pkgname=gifski
pkgver=1.12.2
pkgrel=1
pkgdesc='GIF encoder based on libimagequant (pngquant). Squeezes maximum possible quality from the awful GIF format.'
arch=('x86_64')
url='https://gif.ski'
license=('AGPL3')
depends=('ffmpeg')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ImageOptim/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('0a9287cefd0afceeb5614645c6e7777f0f088a7dd7429186ed2343db41ca1b1eea55effabfe61312dc8888a159e6ee98942a90e47e0b7510cc6913e693f6884c')
options=('!lto')

prepare() {
  cd $pkgname-$pkgver

  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
