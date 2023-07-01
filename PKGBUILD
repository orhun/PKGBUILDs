# Maintainer: Frederik Schwan <freswa at archlinux dot org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=rustypaste
pkgver=0.11.1
pkgrel=1
pkgdesc='A minimal file upload/pastebin service'
arch=('x86_64')
url='https://github.com/orhun/rustypaste'
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
backup=('etc/rustypaste/config.toml')
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/orhun/rustypaste/archive/refs/tags/v${pkgver}.tar.gz)
b2sums=('076caee00477540d0a2b3e4fa8f5df0cbeb691fa1e6411a0739952a3301d4b4b037372844e91abe39f15887b30500fcfed59c80afee167cdd5182ee2a886a07d')

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
