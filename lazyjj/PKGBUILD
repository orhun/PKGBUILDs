# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=lazyjj
pkgver=0.2.0
pkgrel=1
pkgdesc="TUI for Jujutsu/jj"
arch=('x86_64')
url="https://github.com/Cretezy/lazyjj"
license=('Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo-nightly')
checkdepends=('jujutsu')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('098b4d31e4b6ff96a6ab2caf55a953bd7dbbf7eea9c394ffa6367db7febdb72e9639250ab6ddb9058299712dce07264862dc3857735cb3564fb2751149d712ba')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=nightly
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=nightly
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  export RUSTUP_TOOLCHAIN=nightly
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
