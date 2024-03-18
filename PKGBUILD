# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Maxim Baz <archlinux at maximbaz dot com>

pkgname=xplr
pkgver=0.21.7
pkgrel=1
pkgdesc="A hackable, minimal, fast TUI file explorer"
arch=('x86_64')
url="https://github.com/sayanarijit/xplr"
license=('MIT')
depends=('gcc-libs' 'hicolor-icon-theme' 'luajit')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver.tar.gz.asc::$url/releases/download/v${pkgver}/source.tar.gz.asc")
sha512sums=('76486fe388e2a066071ed59c463244a91474106739957637783c601c9a9284931217a9bdff3ab04641d060c1a4b2f5193a54d68ca3beaa2880c1a166b88a9193'
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
