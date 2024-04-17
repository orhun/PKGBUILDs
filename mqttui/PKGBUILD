# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=mqttui
pkgver=0.21.0
pkgrel=1
pkgdesc="Subscribe to a MQTT Topic or publish something quickly from the terminal"
arch=('x86_64')
url="https://github.com/EdJoPaTo/mqttui"
license=('GPL-3.0-or-later')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('64453143e36f59a2fbb0dd67b02437b170d82fa15daf492cff2750cce0f5c126')
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
