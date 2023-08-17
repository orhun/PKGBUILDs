# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=arduino-language-server
pkgver=0.7.5
pkgrel=1
pkgdesc="An Arduino Language Server based on Clangd to Arduino code autocompletion"
arch=('x86_64')
url="https://github.com/arduino/arduino-language-server"
license=('AGPL3')
depends=('glibc' 'arduino-cli' 'clang')
makedepends=('go')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha512sums=('ad8dfa5edfc577d718065687dafa5a3d3bdf6f5f571b1314f6cc8b710c08e49c4920624c2cddfd09ff425536888005cc868414ec5d56032513695a6fec19bc29')

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
