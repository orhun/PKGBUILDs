# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyohei Uto <im@kyoheiu.dev>

pkgname=felix-rs
_pkgname=felix
pkgver=2.12.1
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
sha512sums=('30ff3277d7e9c0c90387a91ed6c50ab1949905ccd645e9e95d2a56a0fd919e9e8bbb69ce4b72525f0e8ed775882840f3829e4387a39a2d2e760d8d1245d7e8c8')
options=('!lto')

prepare() {
  cd "$_pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
