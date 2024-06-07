# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Marco Rubin <marco.rubin@protonmail.com>

pkgname=markuplinkchecker
_name=mlc
pkgver=0.17.1
pkgrel=1
pkgdesc="Check for broken links in markup files"
arch=('x86_64')
url='https://github.com/becheran/mlc'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
b2sums=('269f7620c90fd3c9132e5f5379eb21f183aaf3e6ad19afb40582a59770f6d43cde5adbe2bcf4f8cc5aff99c3227f0f43b5d53a50aa3cd6f1176c00a4a5090b3f')
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
