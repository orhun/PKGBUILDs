# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-run-bin
_pkgname=cargo-bin
pkgver=1.7.3
pkgrel=1
pkgdesc="Build, cache, and run CLI tools scoped in Cargo.toml"
arch=('x86_64')
url='https://github.com/dustinblackman/cargo-run-bin'
license=('MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('522c5e22f89ee8e1abffb16ff6a54b7c2566ba40b4a218ad2f01f22455c4233c')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

# <https://github.com/dustinblackman/cargo-run-bin/issues/18>
# check() {
#   cd "$pkgname-$pkgver"
#   cargo test --frozen
# }

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
