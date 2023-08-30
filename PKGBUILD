# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=httplz
_pkgname=http
pkgver=1.13.2
pkgrel=1
pkgdesc="Host These Things Please - a basic http server for hosting a folder fast and simply"
arch=('x86_64')
url="https://github.com/thecoshman/http"
license=('MIT')
depends=('openssl' 'bzip2')
makedepends=('cargo' 'ruby-ronn-ng')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "Cargo.lock")
sha512sums=('76d23212ca4655adc43f9974472f3441b1f04038b18d7720a8eb06f528cc73891b9fd91d0548b7e2f986152c529a7e9d0629c6c30bd7c838cda1b2e542a5c1e3'
            'e20338a3c6d1a70e61249d59e5466378bcd279d289b0fa6d864a32cb7590041e78aa122690bb62805c48bb1382731e610adfc92da449fd3d32dad8ca12d9f2f7')

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
