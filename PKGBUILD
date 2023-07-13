# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyohei Uto <im@kyoheiu.dev>

pkgname=felix-rs
_pkgname=felix
pkgver=2.5.0
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
sha512sums=('8b7aa28afc7a8ed7c419163c243eb955ca82676f4a0cc3d0f0e28bd45eb67de68f4e472eb4bee5a237f8d714c196497c254af387035bcf07746877db63ef1be0')
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
