# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyohei Uto <im@kyoheiu.dev>

pkgname=felix-rs
_pkgname=felix
pkgver=2.4.0
pkgrel=1
pkgdesc="A TUI file manager with Vim-like key mapping"
arch=('x86_64')
url="https://github.com/kyoheiu/felix"
license=('MIT')
depends=('gcc-libs' 'bzip2')
makedepends=('cargo')
optdepends=('chafa: preview images'
            'zoxide: jump to directories')
checkdepends=('zoxide')
install="$pkgname.install"
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('8cd0854d8a4b6d862a1911d1cc10d097b357104d5fcfd9e5d55d5bf4cf2d8e251063634ffcfd315d1ec3782b5b77869698a658c1d7fda72751708cd4e6a59b2a')
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
