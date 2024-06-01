# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Filipe Nascimento <flipee at tuta dot io>
# Contributor: Sven Lechner <sven[dot]lechner[at]rwth-aachen[dot]de>

pkgname=act
pkgver=0.2.63
pkgrel=1
pkgdesc="Run your GitHub Actions locally"
arch=('x86_64')
url="https://github.com/nektos/act"
license=('MIT')
makedepends=('go')
optdepends=('docker: Connect to local docker')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('67832789cac6d66cf164c31f2d884cccca1343ae07a208f8152fa861f03de5a3')

build() {
  cd $pkgname-$pkgver

  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"

  go build \
      -trimpath \
      -buildmode=pie \
      -mod=readonly \
      -modcacherw \
      -ldflags "-linkmode=external -X main.version=$pkgver"
}

package() {
  cd $pkgname-$pkgver
  install -Dm755 $pkgname -t "$pkgdir/usr/bin"
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
