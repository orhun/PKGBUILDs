# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Marco Rubin <marco.rubin@protonmail.com>

pkgname=markuplinkchecker
_name=mlc
pkgver=0.18.0
pkgrel=1
pkgdesc="Check for broken links in markup files"
arch=('x86_64')
url='https://github.com/becheran/mlc'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('77e64ed2d0691c0644368ded44a05ec9ecc3273b3628aca891936a89a5f40cf4b56b612127ddbfb1c1d5e9d31476518239eae0d27836e41cce5d0bb2dadbe388')
options=('!lto')

prepare() {
  cd $_name-$pkgver
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd $_name-$pkgver
  cargo build --frozen --release
}

check() {
  cd $_name-$pkgver
  cargo test --frozen -- --skip "link_validator::file_system::test::remove_dot"
}

package() {
  cd $_name-$pkgver
  install -Dm0755 -t "$pkgdir/usr/bin/" target/release/$_name
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md" 
}

# vim:set ts=2 sw=2 et:
