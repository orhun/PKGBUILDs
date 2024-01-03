# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-bundle-licenses
pkgver=1.3.0
pkgrel=1
pkgdesc="Bundle licensing of Rust dependencies"
url="https://github.com/sstadick/cargo-bundle-licenses"
arch=('x86_64')
license=('Apache' 'MIT')
depends=('cargo' 'gcc-libs')
source=("${pkgname}-${pkgver}.tar.gz::https://crates.io/api/v1/crates/${pkgname}/${pkgver}/download")
sha256sums=('b3033398d3b96d932d8bb3187ff59f123ad472d76be935be11aae6e76be6937c')
b2sums=('7d0efdaac3e9902ef9df564bf5041cb0975d67af4895ef9b14f3923561a7ab9c4599f4229ef3f5795d77f1823af380ea13455bb602e980a65a452c8ff159e8aa')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "${pkgname}-${pkgver}"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
