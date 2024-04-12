# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

pkgname=kmon
pkgver=1.6.5
pkgrel=1
pkgdesc="Linux kernel manager and activity monitor"
arch=('x86_64')
url="https://github.com/orhun/kmon"
license=('GPL3')
depends=('kmod' 'libxcb')
makedepends=('rust' 'python' 'git')
source=("git+${url}.git#tag=v${pkgver}?signed")
sha512sums=('e6d09fcd578c63c4d361ae60cfaae18e93487b1c1c060c13f0d89ff3a4fb9b9e970001f721e893de5f2031a3def8acb5ac46dee8769e7bc43cf0f3639548ec72')
validpgpkeys=('C4B2D24CF87CD188C79D00BB485B7C52E9EC0DC6') # kmon releases <kmonlinux@protonmail.com>

prepare() {
  cd "${srcdir}"/${pkgname}
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${srcdir}"/${pkgname}
  cargo build --release --frozen
}

check() {
  cd "${srcdir}"/${pkgname}
  cargo test --frozen
}

package() {
  cd "${srcdir}"/${pkgname}
  install -Dm 755 "target/release/${pkgname}" -t "${pkgdir}/usr/bin"
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 "target/man/${pkgname}.8" -t "${pkgdir}/usr/share/man/man8"
  install -Dm 644 "target/completions/${pkgname}.bash" "${pkgdir}/usr/share/bash-completion/completions/${pkgname}"
  install -Dm 644 "target/completions/${pkgname}.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"
  install -Dm 644 "target/completions/_${pkgname}" -t "${pkgdir}/usr/share/zsh/site-functions"
}
