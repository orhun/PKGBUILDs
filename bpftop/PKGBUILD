# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: fossdd <fossdd@pwned.life>
# Contributor: Jose Fernandez <josef@netflix.com>

pkgname=bpftop
pkgver=0.5.1
pkgrel=1
pkgdesc="Dynamic real-time view of running eBPF programs"
url='https://github.com/Netflix/bpftop'
license=('Apache-2.0')
arch=('x86_64')
depends=('libelf' 'gcc-libs' 'zlib')
makedepends=('cargo' 'clang')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.zip")
sha256sums=('8b82869af81a4e4709059c200bae99e8b7bd9648d1772ef45ee63f07f90c39a2')
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
