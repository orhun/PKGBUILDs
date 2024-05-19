# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.25.9
pkgrel=1
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('cargo' 'openssl' 'libcurl.so' 'libgit2.so')
makedepends=('clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz")
sha512sums=('6d09880c1577d9a2140563aa1c37a11a15a420cbfb1098658d6b7c07541ffaf1fcec55aa720338564bb4a549cfb5b8fd79b792c2f36fec2982327f873e8d0cb8')
b2sums=('a9f7117cf6523ecfa6e70d4bf020f9043a4038c9a3cfbf0d841c443b41b9fd4de87f99e12881b16a16006d3c8a406bbf76d49850365d39f770d8129b69904d57')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname}-${pkgver}"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo build -p "$pkgname" --frozen --release --no-default-features
}

check() {
  cd "${pkgname}-${pkgver}"
  LIBSSH2_SYS_USE_PKG_CONFIG=1 cargo test -p "$pkgname" --frozen --no-default-features
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" -t "${pkgdir}/usr/bin"

  install -Dm644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set ts=2 sw=2 et:
