# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Philipp A. <flying-sheep@web.de>

pkgname=cargo-generate
pkgver=0.20.0
pkgrel=1
pkgdesc="Use pre-existing git repositories as templates"
arch=('x86_64')
url="https://github.com/cargo-generate/cargo-generate"
license=('MIT' 'Apache-2.0')
depends=('cargo' 'curl' 'libgit2' 'libssh2' 'openssl')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('7ef6c621fb5487de9b145ea0bc15e06d28964d632e1dab80eaa20f451687c1c2')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo build --release --frozen --no-default-features
}

check() {
  cd "$pkgname-$pkgver"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo test --frozen --lib --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
