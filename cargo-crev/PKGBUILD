# Maintainer: kpcyrd <git@rxv.cc>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-crev
pkgver=0.25.5
pkgrel=2
pkgdesc="Scalable, social, Code REView and recommendation system that we desperately need"
url="https://github.com/crev-dev/cargo-crev"
depends=('cargo' 'openssl' 'libcurl.so' 'libgit2.so')
makedepends=('clang')
arch=('x86_64')
license=('MPL' 'Apache' 'MIT')
options=('!lto')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/crev-dev/cargo-crev/archive/v${pkgver}.tar.gz"
        "index-guix-dep.patch")
sha512sums=('621447b0f5e32ed11af3d4e985d77986e94ceb6d6e0359880e70c20120698fb685b64062824fbd0bfffd9de565a6d5894788996c74637444d7bbdb47ed8e3807'
            '7e1b4dfe843bd1b349598cdb9d6dae66b940a3f71f77965c45f976b9cc259385bd0832d3cdafeef90d5e2dee494e9d13785abaa0626790acc45ba8939b47e5b2')
b2sums=('da2bb5518d1bc9205f8a39827a85e07ada793262ac3050e44cef181629360eb4c6db6db17cdabe35eda0ca3926c1ae2bcd19905559322d11df560612681f1cf0'
        '16279527f28cf5e2b0d48c697e3e4d8219ed671f5a0d08601d1b8b0b1b94ea6cc6198bb8a635beac0d24e0a95ec5b683b3f452c1688b2dfbbb3e56d5311c541e')

prepare() {
  cd "${pkgname}-${pkgver}"
  # https://github.com/crev-dev/cargo-crev/issues/690
  patch -Np1 -i "$srcdir/index-guix-dep.patch"
  cargo fetch --target "$CARCH-unknown-linux-gnu" # --locked
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
