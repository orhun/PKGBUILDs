# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andrew Sun <adsun701 at gmail dot com>
# Contributor: Bruce Zhang <zttt183525594 at gmail dot com>

pkgname=mcfly
pkgver=0.9.1
pkgrel=1
pkgdesc="Fly through your shell history"
arch=('x86_64')
url="https://github.com/cantino/mcfly"
license=('MIT')
depends=('sh')
optdepends=('zsh: for zsh support'
            'fish: for fish support')
makedepends=('cargo')
install=mcfly.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('3f2f7ff1d8c4ccf5e7f98b185723c415a38883068cb8533ddd551ed4a8f059e9')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"

  install -Dm 644 "$pkgname.bash" -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "$pkgname.zsh" -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_conf.d"
}

# vim: ts=2 sw=2 et:
