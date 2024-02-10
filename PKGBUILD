# Maintainer: Filipe Laíns (FFY00) <lains@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp Wolfer <ph.wolfer@gmail.com>

pkgname=gifski
pkgver=1.14.4
pkgrel=1
pkgdesc='GIF encoder based on libimagequant (pngquant). Squeezes maximum possible quality from the awful GIF format.'
arch=('x86_64')
url='https://gif.ski'
license=('AGPL3')
depends=('ffmpeg')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ImageOptim/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('28f7d6916f1afecaf9c95f9c6a45668062e273718ca38cb31b3e2f967d965bd193b396d75f510e38ed0d72a9cc8b2e3278ff32ed2cc93627a4f8b603a4a47e57')
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
