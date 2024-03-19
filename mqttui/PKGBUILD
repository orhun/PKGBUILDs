# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=mqttui
pkgver=0.20.0
pkgrel=2
pkgdesc="Subscribe to a MQTT Topic or publish something quickly from the terminal"
arch=('x86_64')
url="https://github.com/EdJoPaTo/mqttui"
license=('GPL-3.0-or-later')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('f6b625ae76fcabb4b3c31b8b0302debc4df4d34934da6152dcc6f8d26a17a57d')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd $pkgname-$pkgver
  install -Dm755 target/release/$pkgname -t "${pkgdir}/usr/bin"
  install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}/"
  install -Dm644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}/"
  install -Dm644 CHANGELOG.md -t "${pkgdir}/usr/share/doc/${pkgname}/"

  install -Dm644 "target/completions/${pkgname}.bash" -t "${pkgdir}/usr/share/bash-completion/completions/"
  install -Dm644 "target/completions/${pkgname}.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d/"
  install -Dm644 "target/completions/_${pkgname}" -t "${pkgdir}/usr/share/zsh/site-functions/"

  for man in target/manpages/*; do
	  install -Dm644 "$man" -t "${pkgdir}/usr/share/man/man1/"
  done
}

# vim:set ts=2 sw=2 et:
