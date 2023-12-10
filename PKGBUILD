# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Ellie Huxtable <e@elm.sh>

pkgname=atuin
pkgver=17.1.0
pkgrel=1
pkgdesc="Magical shell history"
arch=('x86_64')
url="https://github.com/atuinsh/atuin"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
optdepends=('bash-preexec: bash integration')
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('6a0b1542e7061e6a5bcdf3c284d3ad386e3504e040fcfa1500f530a5125b37b8')
options=('!lto')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir completions/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --all-features
  for sh in 'bash' 'fish' 'zsh'; do
    "target/release/$pkgname" gen-completions -s "$sh" -o completions/
  done
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all-features --workspace --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "completions/$pkgname.bash" "${pkgdir}/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "${pkgdir}/usr/share/zsh/site-functions"
}

# vim: ts=2 sw=2 et:
