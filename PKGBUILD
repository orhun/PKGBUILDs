# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyohei Uto <im@kyoheiu.dev>

pkgname=felix-rs
_pkgname=felix
pkgver=2.11.0
pkgrel=1
pkgdesc="A TUI file manager with Vim-like key mapping"
arch=('x86_64')
url="https://github.com/kyoheiu/felix"
license=('MIT')
depends=('gcc-libs' 'bzip2')
makedepends=('cargo')
optdepends=('chafa: preview images'
            'zoxide: jump to directories'
            'bat: syntax highlighting')
checkdepends=('zoxide')
install="$pkgname.install"
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f0d4d707b72a14c4ca218d1d18e11a22ebd884d60d800a9663e579a3e3b085079f381127d4cf564d56166330f4c28e3afa60ecf99eb2dc2d4139fcb71c22a729')
options=('!lto')

prepare() {
  cd "$_pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$_pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$_pkgname-$pkgver"
  # https://github.com/kyoheiu/felix/issues/200
  touch testfiles/permission_test
  chmod 444 testfiles/permission_test
  cargo test --frozen
}

package() {
  cd "$_pkgname-$pkgver"
  install -Dm 755 "target/release/fx" "$pkgdir/usr/bin/$_pkgname"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
