# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=systeroid
pkgver=0.4.2
pkgrel=1
pkgdesc="A more powerful alternative to sysctl"
arch=('x86_64')
url="https://github.com/orhun/systeroid"
license=('MIT' 'Apache')
depends=('libxcb' 'libxkbcommon' 'linux-docs')
makedepends=('cargo' 'python')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('0421c50f8d874b69c1ac1b27fc698d436a92bb80d67e6abdd55ab8abd034b881e6832c27ccb18ee184b690d394d1bbf4469705808b585ea98737601ec277521e')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  NO_COLOR=1 cargo test --frozen --no-default-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 755 "target/release/$pkgname-tui" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man8/$pkgname.8" -t "$pkgdir/usr/share/man/man8"
  install -Dm 644 "man8/$pkgname-tui.8" -t "$pkgdir/usr/share/man/man8"
}

# vim: ts=2 sw=2 et:
