# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Maxim Baz <$pkgname at maximbaz dot com>

pkgname=xplr
pkgver=0.21.5
pkgrel=1
pkgdesc="A hackable, minimal, fast TUI file explorer"
arch=('x86_64')
url="https://github.com/sayanarijit/xplr"
license=('MIT')
depends=('gcc-libs' 'hicolor-icon-theme' 'luajit')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver.tar.gz.asc::$url/releases/download/v${pkgver}/source.tar.gz.asc")
sha512sums=('4f6323d123e3963c1b427df55200771f2d3cf2d8cfc07dac488d513215030bf98c96bdcbdf5b801f319afd3fd780c82abfbc6b212a6178bdfae86f798dd0f0df'
            'SKIP')
validpgpkeys=('D59CA14710C17C6B24717AF90F8EF5258DC38077') # Arijit Basu (June 3, 2021)
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  sed -i "s/features = \['luajit', 'vendored', 'serialize', 'send'\]/features = \['luajit', 'serialize', 'send'\]/g" Cargo.toml
  cargo update -p mlua
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --locked --release
}

check() {
  cd "$pkgname-$pkgver"

  # unit tests need the binary, so build it first.
  # building in debug mode (both bin and tests) in order to not overwrite the binary produced in build() that we will later package
  cargo build --locked
  cargo test --locked
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
