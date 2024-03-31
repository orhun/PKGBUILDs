# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgname=trippy
pkgver=0.10.0
pkgrel=1
pkgdesc='A network diagnostic tool'
arch=('x86_64')
url='https://trippy.cli.rs'
license=('Apache-2.0')
depends=('gcc-libs' 'libcap')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/fujiapple852/trippy/archive/$pkgver.tar.gz")
b2sums=('08cc2bc288b78fa205954db245c89fd5ce1966ac497dd8108feb816b737035f010ab5b92dda733962408ec039f4afff2d2c07505ed7f9ffe2577c545c5f0d161')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
  local compgen="target/release/trip --generate"
  $compgen bash >"completions/$pkgname"
  $compgen fish >"completions/$pkgname.fish"
  $compgen zsh >"completions/_$pkgname"
}

check() {
  cd $pkgname-$pkgver
  cargo test --frozen
}

package() {
  cd $pkgname-$pkgver
  install -Dm 755 -t "$pkgdir"/usr/bin target/release/trip
  install -Dm 644 -t "$pkgdir"/usr/share/doc/"$pkgname" README.md
  install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}
