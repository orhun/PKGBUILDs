# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jose Fernandez <josef@netflix.com>

pkgname=bpftop
pkgver=0.5.0
pkgrel=2
pkgdesc="Dynamic real-time view of running eBPF programs"
url='https://github.com/Netflix/bpftop'
license=('Apache-2.0')
arch=('x86_64')
depends=('libelf' 'gcc-libs' 'zlib')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.zip")
sha256sums=('f22431b9da320a3421c7fca17be1068e5f6d5797bd2cfda6caab10dc24723dd9')
options=('!lto')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "target/release/$pkgname" -t "$pkgdir/usr/bin/"
  install -Dm644 'LICENSE' -t "$pkgdir/usr/share/licenses/$pkgname/"
  install -Dm644 'README.md' -t "$pkgdir/usr/share/doc/$pkgname/"
}

# vim: ts=2 sw=2 et:
