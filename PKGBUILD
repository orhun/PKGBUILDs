# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Amin Vakil <info AT aminvakil DOT com>

pkgname=actionlint
pkgver=1.6.26
pkgrel=2
pkgdesc="Static checker for GitHub Actions workflow files"
arch=('x86_64')
url="https://github.com/rhysd/actionlint"
license=('MIT')
makedepends=('go' 'git')
optdepends=('python-pyflakes' 'shellcheck')
source=("${pkgname}-${pkgver}-${pkgrel}.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('507d771f4c863bf98dfe1db3500a4c9344e3a35592a6e2ac4183f00a63291feb')

prepare(){
  cd "$pkgname-$pkgver"
  mkdir -p build/
}

build() {
  cd "$pkgname-$pkgver"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
  go build -ldflags "-X github.com/rhysd/actionlint.version=$pkgver" -o build ./cmd/${pkgname}
}

check() {
  cd "$pkgname-$pkgver"
  # To run tests for actionlint, `.git` directory is needed.
  # actionlint finds a root of repository by checking the directory.
  mkdir -p .git
  go test -v ./...
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 build/$pkgname "$pkgdir"/usr/bin/$pkgname
  install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 LICENSE.txt -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
