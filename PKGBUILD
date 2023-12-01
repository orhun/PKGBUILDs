# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Morteza NourelahiAlamdari <m@0t1.me>

pkgname=binocle
pkgver=0.3.2
pkgrel=1
pkgdesc="A graphical tool to visualize binary data"
arch=('x86_64')
url="https://github.com/sharkdp/binocle"
license=('MIT' 'Apache')
depends=('gcc-libs')
makedepends=('rust')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('d4d2e225723e72d991eac9dc91c0056c902eeabbe046161447c4a8a4e3200515b5dfd93dbeabf0cdd420f9eee8a3f7e0e2f0a054cfb988cfd10a3b09c43f20f3')

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
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
