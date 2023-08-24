# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=httplz
_pkgname=http
pkgver=1.13.1
pkgrel=1
pkgdesc="Host These Things Please - a basic http server for hosting a folder fast and simply"
arch=('x86_64')
url="https://github.com/thecoshman/http"
license=('MIT')
depends=('openssl' 'bzip2')
makedepends=('cargo' 'ruby-ronn-ng')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "Cargo.lock")
sha512sums=('3f5a018e63b1736141c7aeae9e3f3098d14cc4b8ce66fbc3bbc9bb9ae207d13cd0a81509a85c5d209c24938a0f8d0327c21a3cdf7b46ce3c7e788dd4dff9f04f'
            '2ab99ac36f7497439829004e68d53b56ba74d54c80c698f8ec21c0235ed87a3c0a063af5bc4ac270a2e859ada561d86fb37dec59b06d0a10c9ec43729fcc51d6')

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
