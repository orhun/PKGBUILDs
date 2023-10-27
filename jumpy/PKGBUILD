# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kleintux <reg-archlinux AT klein DOT tuxli DOT ch>

pkgname=jumpy
pkgver=0.8.2
pkgrel=1
pkgdesc="Tactical 2D shooter in fishy pixels style"
arch=('x86_64')
url="https://fishfolk.org/games/jumpy"
license=('MIT' 'Apache')
depends=('pkg-config' 'mesa-libgl' 'alsa-lib' 'systemd-libs' 'libudev.so')
makedepends=('cargo' 'systemd')
replaces=('fishfight')
source=("$pkgname-$pkgver.tar.gz::https://github.com/fishfight/jumpy/archive/v$pkgver.tar.gz"
        "$pkgname.sh")
sha512sums=('492cd8945eb8b487152c635884618a7004fa09e1628f3bbc86f04faa096daab231aef278fd21cf4779caf5240e1e6fb940a7c802c3d917c905860080abb76d96'
            '182567c5b24c2a10a233d6b5e17ef9a0c28893e966f5f9536fb5b64acbae68312e96867f3648d4b694d011d020d8e25e2616d699df5c3dbd8d66d5902eaafbe7')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/lib"
  install -Dm 755 "$srcdir/$pkgname.sh" "$pkgdir/usr/bin/$pkgname"

  mkdir -p "$pkgdir/opt/$pkgname"
  cp -r "assets" "$pkgdir/opt/$pkgname/"
  find "$pkgdir/opt/$pkgname/assets/music/" -type f -exec chmod 444 {} \;
  find "$pkgdir/opt/$pkgname/assets/player/sounds/" -type f -exec chmod 444 {} \;

  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 licenses/LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
