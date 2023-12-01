# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgname=trippy
pkgver=0.9.0
pkgrel=1
pkgdesc='A network diagnostic tool'
arch=('x86_64')
url='https://trippy.cli.rs'
license=('Apache')
depends=('gcc-libs' 'libcap')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::https://github.com/fujiapple852/trippy/archive/$pkgver.tar.gz")
b2sums=('92135376948ad710f14a2c8326e938f5ae0fa47563aea588b678dc0e55752c73d56d0468623345e0240b5f6061ebf11efea0b309f33dc738b2895901fc422d4a')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
