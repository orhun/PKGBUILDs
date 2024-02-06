# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=arduino-language-server
pkgver=0.7.6
pkgrel=1
pkgdesc="An Arduino Language Server based on Clangd to Arduino code autocompletion"
arch=('x86_64')
url="https://github.com/arduino/arduino-language-server"
license=('AGPL3')
depends=('glibc' 'arduino-cli' 'clang')
makedepends=('go')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('fb8c2d4df3337caecd3352cadc0a3ce780ae1f94a2b40ed8ebbda93cd5054fcebefaf049d24f2a11ac7b6fdc9e2b90817da0ebf36772a2ca055dda8e0a5e7be8')

build() {
  cd "$pkgname-$pkgver"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
  go build -o "$pkgname" .
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
