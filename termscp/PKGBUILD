# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Christian Visintin <christian dot visintin at gmail dot com>
# Contributor: Luis Martinez <luis dot martinez at tuta dot io>

pkgname=termscp
pkgver=0.14.0
pkgrel=1
pkgdesc="A feature rich terminal UI file transfer and explorer"
arch=('x86_64')
url="https://github.com/veeso/termscp"
license=('MIT')
depends=('gcc-libs' 'zlib' 'openssl' 'dbus' 'smbclient')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('8d23cfd36fa832c22bf7819506e913121fe310da5a31ecc2c6a39d78fd2f354ef6889288eaeed69a45ecd82e66b0cb0220e3a6474154042d85ceb7d6804d7cb3')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- \
    --skip system::environment::tests::test_system_environment_get_config_dir_err \
    --skip system::keys::keyringstorage::tests::test_system_keys_keyringstorage \
    --skip system::environment::tests::test_system_environment_get_config_dir
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
