# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Wenxuan Zhang <wenxuangm@gmail.com>

pkgname=rust-script
pkgver=0.34.0
pkgrel=1
pkgdesc='Run Rust files and expressions as scripts without any setup or compilation'
arch=('x86_64')
url='https://rust-script.org'
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://github.com/fornwall/rust-script/archive/$pkgver.tar.gz")
sha256sums=('490a41bc1fd5312c5992df44dfc1e61002a046646bc4cce19412d020b2e25005')

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
