# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jameson Pugh <imntreal@gmail.com>
# Contributor: Mikaela Szekely <qyriad@gmail.com>

pkgname=cargo-update
pkgver=13.2.1
pkgrel=1
pkgdesc="A cargo subcommand for checking and applying updates to installed executables"
arch=('x86_64')
url="https://github.com/nabijaczleweli/cargo-update"
license=('MIT')
depends=('gcc-libs' 'zlib' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('e5d5bab0812bc929caed93aa70f041e58e006b63c58ff4c5e3d4fa36117a904f'
            '009d3703a6c3580b951267d769030e31c3df4ba20f6a62acbe253ce9405a4840')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/cargo-install-update" "$pkgdir/usr/bin/cargo-install-update"
  install -Dm755 "target/release/cargo-install-update-config" "$pkgdir/usr/bin/cargo-install-update-config"

  install -Dm644 "man/cargo-install-update.md" "$pkgdir/usr/share/doc/${pkgname}/cargo-install-update.md"
  install -Dm644 "man/cargo-install-update-config.md" "$pkgdir/usr/share/doc/${pkgname}/cargo-install-update-config.md"
  install -Dm644 "README.md" "$pkgdir/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
