# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Maxim Baz <archlinux at maximbaz dot com>

pkgname=xplr
pkgver=0.21.9
pkgrel=1
pkgdesc="A hackable, minimal, fast TUI file explorer"
arch=('x86_64')
url="https://github.com/sayanarijit/xplr"
license=('MIT')
depends=('gcc-libs' 'hicolor-icon-theme' 'luajit')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver.tar.gz.asc::$url/releases/download/v${pkgver}/source.tar.gz.asc")
sha512sums=('683879d3bd1f118700d0ee53bc76aa9c4f887e58749dcb6805471309c5b2de1d3ce5206c77c1335aabdd13e6f2349aff7293c17a99957921ccdfc7e9cbf1771d'
            'SKIP')
validpgpkeys=('D59CA14710C17C6B24717AF90F8EF5258DC38077') # Arijit Basu (June 3, 2021)
options=('!lto')

build() {
  cd "$pkgname-$pkgver"
  # disable vendored-lua feature, the same below
  cargo build --locked --release --no-default-features
}

check() {
  cd "$pkgname-$pkgver"

  # unit tests need the binary, so build it first.
  # building in debug mode (both bin and tests) in order to not overwrite the binary produced in build() that we will later package
  cargo build --locked --no-default-features
  cargo test --locked --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 docs/en/src/* -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 src/init.lua -t "$pkgdir/usr/share/$pkgname/examples"
  install -Dm 644 "assets/desktop/$pkgname.desktop" -t "$pkgdir/usr/share/applications"
  for i in 128 16 32 64; do
    install -Dm 644 "assets/icon/${pkgname}${i}.png" "$pkgdir/usr/share/icons/hicolor/${i}x${i}/apps/${pkgname}.png"
  done
  install -Dm 644 "assets/icon/$pkgname.svg" -t "$pkgdir/usr/share/icons/hicolor/scalable/apps"
}

# vim:set ts=2 sw=2 et:
