# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Marco Rubin <marco.rubin@protonmail.com>

pkgname=markuplinkchecker
_name=mlc
pkgver=0.17.0
pkgrel=1
pkgdesc="Check for broken links in markup files"
arch=('x86_64')
url='https://github.com/becheran/mlc'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('46aace2e75bbd9781e6cd0a27dfb3dfec370fe49b8867818f46eaf77ec932f98ec888cd2aacc1fc81119306dcafa3e45010724eab2ede4e098edee5b306fec94')
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
