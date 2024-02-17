# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=gping
pkgver=1.16.1
pkgrel=1
pkgdesc="Ping, but with a graph"
arch=('x86_64')
url="https://github.com/orf/gping"
license=('MIT')
depends=('iputils')
makedepends=('cargo' 'libgit2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('848f714beb692ae859e2eb99c78671830c46f2d8775a47163d5c61d040c3d9856ec07b35c613f6c4e4edc99b71c494ee482d5bf044e83abd9f1843fea123b880')
options=('!lto')

prepare() {
  mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"
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
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 readme.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
