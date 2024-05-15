# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kxxt <rsworktech at outlook dot com>

pkgname=tracexec
pkgver=0.2.2
pkgrel=1
pkgdesc="A small utility for tracing execve{,at} and pre-exec behavior"
arch=('x86_64')
url="https://github.com/kxxt/tracexec"
license=('GPL-2.0-or-later')
depends=('gcc-libs')
makedepends=('cargo' 'cargo-about' 'git')
source=("$pkgname-$pkgver::git+https://github.com/kxxt/tracexec.git#tag=v$pkgver")
b2sums=('3b997bc595f599da759a5d39eccbdf849b2f30a090bf6f960ada6b5aa829e06166d899b8388d775dff8ccfe591abb15f7802527b8273e1fe4833ad97c1462212')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  # --bins: needed for test
  cargo build --bins --frozen --release --all-features
  cargo about generate -o THIRD_PARTY_LICENSES.HTML about.hbs
}

check() {
  cd "$pkgname-$pkgver"
  RUST_TEST_THREADS=1 cargo test --frozen --release --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 THIRD_PARTY_LICENSES.HTML "$pkgdir/usr/share/licenses/$pkgname/THIRD_PARTY_LICENSES.HTML"
}

# vim:set ts=2 sw=2 et:
