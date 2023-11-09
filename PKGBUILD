# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jameson Pugh <imntreal@gmail.com>
# Contributor: Mikaela Szekely <qyriad@gmail.com>

pkgname=cargo-update
pkgver=13.2.0
pkgrel=1
pkgdesc="A cargo subcommand for checking and applying updates to installed executables"
arch=('x86_64')
url="https://github.com/nabijaczleweli/cargo-update"
license=('MIT')
depends=('gcc-libs' 'zlib' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('0c2495b7f9cf1409b13f54615a07a71c09d5099f71c2c00ce7c26ccc88112691'
            '5a34f38b04f0d780ef68da3fa0b6cb3068641222dca59f30dad7851c10f3ba33')
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
