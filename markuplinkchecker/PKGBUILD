# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Marco Rubin <marco.rubin@protonmail.com>

pkgname=markuplinkchecker
_name=mlc
pkgver=0.17.2
pkgrel=1
pkgdesc="Check for broken links in markup files"
arch=('x86_64')
url='https://github.com/becheran/mlc'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('3133d87cb2a44cb4deb5dc5ece237f259f493ca8fdc6f0f4a1dd4680828f48ed7c4e2edfa6ae86ffadf2daaf16ea1feec5b4abec614ad369b9f8c86df02150e1')
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
