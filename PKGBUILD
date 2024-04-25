# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Relwi <theofficialdork@hotmail.com>

pkgname=twitch-tui
_pkgname=twt
pkgver=2.6.7
pkgrel=1
pkgdesc="Twitch chat in the terminal"
arch=('x86_64')
url="https://github.com/Xithrius/twitch-tui"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('986c74a006acaf72407d114171b719f1ba88ac32d77583777206648c2464ccd6f632f3b737135e4b95c985b599c82eb0c908f4a5f72d13fec802dffd4bf225a8')
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
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$_pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim: ts=2 sw=2 et:
