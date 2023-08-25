# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Kyohei Uto <im@kyoheiu.dev>

pkgname=felix-rs
_pkgname=felix
pkgver=2.8.1
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
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver-cargo-lock.patch::$url/commit/f6696fc5ddeeac791a562b7c27517eed0fd9ee15.patch")
sha512sums=('7ca339be09a16306894a25a0d773bd3109048363743276629cf1749ac99f9b242616699cd22e02bf35ce53273c69628769f9633ecce2be3aea48ba0d868418c1'
            '350dab9229e3ec638989f1f5aa63ef4a996da3cedf8f6186a84aca317864b994c7355e2faa51385099aae923d2d062084440b755db04cdd5f7967af953720b33')
options=('!lto')

prepare() {
  cd "$_pkgname-$pkgver"
  patch -Np1 -i "../$pkgname-$pkgver-cargo-lock.patch"
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
