# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Wenxuan Zhang <wenxuangm@gmail.com>

pkgname=rust-script
pkgver=0.29.0
pkgrel=1
pkgdesc='Run Rust files and expressions as scripts without any setup or compilation'
arch=('x86_64')
url='https://rust-script.org'
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/fornwall/rust-script/archive/$pkgver.tar.gz")
sha256sums=('d1092bd93ccc25f98ba92735b8a23b80c130d4c2ca367d44fce93c4669ffb446')

prepare() {
  cd "$pkgname-$pkgver"

  # download dependencies
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"

  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"

  cargo test \
	--frozen -- \
	--skip "tests::script::test_nightly_toolchain" \
	--skip "tests::script::test_stable_toolchain"
}

package() {
  cd "$pkgname-$pkgver"

  # binary
  install -vDm755 -t "$pkgdir/usr/bin" "target/release/$pkgname"

  # documentation
  install -vDm644 -t "$pkgdir/usr/share/doc/$pkgname" README.md

  # licenses
  install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE*
}
