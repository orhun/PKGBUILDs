# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: mark.blakeney at bullet-systems dot net
# Contributor: David Birks <david@birks.dev>
# Contributor: David Stark <david@starkers.org>

pkgname=dive
pkgver=0.12.0
pkgrel=1
pkgdesc="A tool for exploring layers in a docker image"
arch=('x86_64')
url="https://github.com/wagoodman/dive"
license=('MIT')
depends=('glibc')
makedepends=('go')
checkdepends=('python')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('2b69b8d28220c66e2575a782a370a0c05077936ae3ce69180525412fcca09230')

build() {
  cd $pkgname-$pkgver
  go build \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-X main.version=$pkgver -linkmode external -extldflags \"${LDFLAGS}\"" \
    -o bin/dive \
    .
}

check() {
  cd "$pkgname-$pkgver"
  make test
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "bin/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 LICENSE  -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim:set ts=2 sw=2 et:
