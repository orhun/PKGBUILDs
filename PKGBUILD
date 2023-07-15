# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cyqsimon <28627918+cyqsimon@users.noreply.github.com>

pkgname=httplz
_pkgname=http
pkgver=1.13.0
pkgrel=1
pkgdesc="Host These Things Please - a basic http server for hosting a folder fast and simply"
arch=('x86_64')
url="https://github.com/thecoshman/http"
license=('MIT')
depends=('openssl' 'bzip2')
makedepends=('cargo' 'ruby-ronn-ng')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz"
        "Cargo.lock")
sha512sums=('de11dbcb5494354b27dde4489142ef7fc722a83246ef2f5a7bc040c5137fadd5ed49aabbfe49d303eb45f48b9face5997bf88e3394bec7dfd55403aaf8f63fb6'
            'f2d68eb43aee805117cfe5d4dbd27a90273ee48155342042423946339740e457d99f023183cf9801e7ead17654f6d0dfa8f3d80da420fb8e0bef265bc79031b1')

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
