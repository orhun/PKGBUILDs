# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kleintux <reg-archlinux AT klein DOT tuxli DOT ch>

pkgname=jumpy
pkgver=0.9.0
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
sha512sums=('6ee46987c56f40afdfac986c5b9a00d98064a749532f93f457fd68b8cbc63b7b6ebbb4c421b9b5cc55e7f48f10cc1011aa7f796bb217e58b362ce2518a9e45b5'
            'c03ee6a44bcbd06618526005f87b4afc8247d6bc08f5a56cc1932546067cc7e4ec0de2def92f427e86888d994f5496bf40187beaca8777b92b2499c306246c71')
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
  cp -r "packs" "$pkgdir/opt/$pkgname/"
  find "$pkgdir/opt/$pkgname/assets/music/" -type f -exec chmod 444 {} \;
  find "$pkgdir/opt/$pkgname/assets/player/sounds/" -type f -exec chmod 444 {} \;

  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 licenses/LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
