# Maintainer: Frederik Schwan <freswa at archlinux dot org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rustypaste
pkgver=0.10.0
pkgrel=1
pkgdesc='A minimal file upload/pastebin service'
arch=('x86_64')
url='https://github.com/orhun/rustypaste'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
backup=('etc/rustypaste/config.toml')
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/orhun/rustypaste/archive/refs/tags/v${pkgver}.tar.gz)
b2sums=('de078361bbd7b4b1482c01f374c189f6704ca0f96515c6faa36243ebed9c8dc42f50eff3f5ae0f4d8dcccc250f5e82ffc560100d0d235f0234ef9a6ba3bff85c')

prepare() {
  cd ${pkgname}-${pkgver}
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd ${pkgname}-${pkgver}
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  CFLAGS+=' -ffat-lto-objects'
  cargo build --release --frozen --no-default-features --features openssl
}

check() {
  cd ${pkgname}-${pkgver}
  export RUSTUP_TOOLCHAIN=stable
  CFLAGS+=' -ffat-lto-objects'
  cargo test --frozen -- --test-threads 1

  cd fixtures
  sed -i "s|target/debug|target/release|" test-fixtures.sh
  ./test-fixtures.sh
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm755 target/release/${pkgname} -t "${pkgdir}"/usr/bin
  install -Dm644 config.toml -t "${pkgdir}"/etc/rustypaste
  install -Dm644 README.md -t "${pkgdir}"/usr/share/doc/${pkgname}
  install -Dm644 LICENSE -t "${pkgdir}"/usr/share/licenses/${pkgname}
  install -Dm644 extra/systemd/rustypaste.env -t "${pkgdir}"/etc/rustypaste
  install -Dm644 extra/systemd/rustypaste.service -t "$pkgdir"/usr/lib/systemd/system/
  install -Dm644 extra/systemd/rustypaste.sysusers "${pkgdir}"/usr/lib/sysusers.d/rustypaste.conf
  install -Dm644 extra/systemd/rustypaste.tmpfiles "${pkgdir}"/usr/lib/tmpfiles.d/rustypaste.conf
}
