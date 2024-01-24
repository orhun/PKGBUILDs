# Maintainer: Frederik Schwan <freswa at archlinux dot org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-deny
pkgver=0.14.10
pkgrel=1
pkgdesc='Cargo plugin for linting your dependencies'
arch=('x86_64')
url='https://github.com/EmbarkStudios/cargo-deny'
license=('MIT' 'Apache-2.0')
depends=('cargo' 'gcc-libs')
makedepends=('git')
options=(!lto)
source=("$pkgname-$pkgver::git+$url.git#tag=$pkgver"
  "$pkgname-advisory-db::git+https://github.com/rustsec/advisory-db"
  "$pkgname-test-advisory-db::git+https://github.com/EmbarkStudios/test-advisory-db")
sha256sums=('SKIP'
            'SKIP'
            'SKIP')

prepare() {
  cd "$pkgname-$pkgver"
  git submodule init
  git config submodule."tests/advisory-db/github.com-2f857891b7f43c59".url "${srcdir}/${pkgname}-advisory-db"
  git config submodule."tests/advisory-db/github.com-c373669cccc50ac0".url "${srcdir}/${pkgname}-test-advisory-db"
  git -c protocol.file.allow=always submodule update --init --recursive
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
  install -Dm755 target/release/cargo-deny -t "${pkgdir}"/usr/bin
  install -Dm644 README.md -t "${pkgdir}"/usr/share/doc/${pkgname}
  install -Dm644 LICENSE-MIT -t "${pkgdir}"/usr/share/licenses/${pkgname}
}
