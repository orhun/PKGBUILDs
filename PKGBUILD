# Maintainer: Jelle van der Waa <jelle@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: CosmicHorror <CosmicHorrorDev@pm.me>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-insta
pkgver=1.36.1
pkgrel=1
pkgdesc="Cargo plugin for snapshot testing in Rust"
url="https://github.com/mitsuhiko/insta"
depends=('gcc-libs' 'cargo')
arch=('x86_64')
license=('Apache-2.0')
source=("$pkgname-$pkgver.tar.gz::https://static.crates.io/crates/$pkgname/$pkgname-$pkgver.crate")
sha512sums=('d5ed286dbded279c26809e62de4b5746d437145c8553a2f091e1a499e80843505bdd9b937ea0f2ecc300f8c2257431567696b541c04130193aefccc23aba895c')

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
