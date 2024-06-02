# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=httplz
_pkgname=http
pkgver=2.0.2
pkgrel=1
pkgdesc="Host These Things Please - a basic http server for hosting a folder fast and simply"
arch=('x86_64')
url="https://github.com/thecoshman/http"
license=('MIT')
depends=('openssl' 'bzip2')
makedepends=('cargo' 'ruby-ronn-ng')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "Cargo.lock")
sha512sums=('41a48fc1ecfb9ac4dcb93db8711db971edbd436bd457309f3a85cf969b97246ca6232a34ea1b4ef345a3672611e29a184d4dccd5a5181604dec9958ad32ea22b'
            '2ed0982c9cd49831551d7ab053a0c78dc7e1ac75748c4890f6a0377607306b352d756e4f40c10b4d85b16d513bb3aac927f3e1b6760ac45a034589ac1d1cbf73')

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
