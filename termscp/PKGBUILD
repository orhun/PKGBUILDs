# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Christian Visintin <christian dot visintin at gmail dot com>
# Contributor: Luis Martinez <luis dot martinez at tuta dot io>

pkgname=termscp
pkgver=0.13.0
pkgrel=2
pkgdesc="A feature rich terminal UI file transfer and explorer"
arch=('x86_64')
url="https://github.com/veeso/termscp"
license=('MIT')
depends=('gcc-libs' 'zlib' 'openssl' 'dbus' 'smbclient')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('1134a29612e893f4c8c7c285312753880925474967a414a3d5ed22a4dcdfa6be71c14bc77107bb99522c6613a30f3704436de5af77ed230492cfcabc51db558d')
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
