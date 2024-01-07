# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Alexander Bruegmann <mail[at]abruegmann[dot]eu>

pkgname=cargo-generate-rpm
pkgver=0.14.0
pkgrel=1
pkgdesc='Cargo helper command to generate a binary RPM package'
arch=('x86_64')
url="https://github.com/cat-in-136/cargo-generate-rpm"
license=('MIT')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('36616e7bb967f459325c9b01651aef7a4250d04b274f50c55b3759a9ab86d76a')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  # https://github.com/cat-in-136/cargo-generate-rpm/issues/60
  cargo fetch --target "$(rustc -vV | sed -n 's/host: //p')" # --locked
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}


check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
