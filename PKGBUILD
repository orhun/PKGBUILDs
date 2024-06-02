# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=httplz
_pkgname=http
pkgver=2.0.1
pkgrel=1
pkgdesc="Host These Things Please - a basic http server for hosting a folder fast and simply"
arch=('x86_64')
url="https://github.com/thecoshman/http"
license=('MIT')
depends=('openssl' 'bzip2')
makedepends=('cargo' 'ruby-ronn-ng')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "Cargo.lock")
sha512sums=('f22aad83dc2d33671e7e9db5e4be130c07636716bae3b7bb09bc81a69cfb860519c1d9aaadd53e91ddd8d8179f9d5cc964dad004f9e42ee48ce71ab276821f46'
            '27f5e4ef0603a80c009d4e2df2b04d117473ff79c684a6dae3b0cd9c8539706f490f96ae07ebd7252b3fdb433586b8834aea35d4bc48843ab9cbf4025c9ead88')

prepare() {
  # https://github.com/thecoshman/http/issues/84
  cp Cargo.lock "${_pkgname}-${pkgver}"
  # fetch dependencies
  cd "${_pkgname}-${pkgver}"
  cargo fetch --locked --target="${CARCH}-unknown-linux-gnu"
  # rename man page
  mv "${_pkgname}.md" "${pkgname}.md"
  mkdir man
}

build() {
  cd "${_pkgname}-${pkgver}"
  # only build and install the `httplz` binary and exclude `http`
  # they are identical and `httplz` is significantly less likely to cause conflicts
  cargo build --release --frozen --bin="$pkgname"
  # generate man page
  ronn --organization="http developers" "${pkgname}.md" -o man
}

check() {
  cd "${_pkgname}-${pkgver}"
  cargo test --frozen
}

package() {
  cd "${_pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "man/${pkgname}.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
