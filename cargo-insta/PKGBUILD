# Maintainer: Jelle van der Waa <jelle@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: CosmicHorror <CosmicHorrorDev@pm.me>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-insta
pkgver=1.37.0
pkgrel=1
pkgdesc="Cargo plugin for snapshot testing in Rust"
url="https://github.com/mitsuhiko/insta"
depends=('gcc-libs' 'cargo')
arch=('x86_64')
license=('Apache-2.0')
source=("$pkgname-$pkgver.tar.gz::https://static.crates.io/crates/$pkgname/$pkgname-$pkgver.crate")
sha512sums=('aea5c06a582ef003a1cb0d269dafd8d5526e8e157ed1c09db561e7e9418f91f5f61bda1771af257dcd5ea05291d9371e7068f832885ae8722b5b2a7cbd530681')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release --all-features
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/$pkgname"
}

# vi: filetype=sh shiftwidth=2 expandtab
