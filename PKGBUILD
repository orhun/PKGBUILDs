# Maintainer: Jelle van der Waa <jelle@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Fabio 'Lolix' Loli <fabio.loli@disroot.org> -> https://github.com/FabioLolix
# Contributor: Moritz Schönherr <moritz.schoenherr@gmail.com>

pkgname=mdbook
pkgver=0.4.33
pkgrel=1
pkgdesc="Create book from markdown files, like Gitbook but implemented in Rust"
url="https://github.com/rust-lang/mdBook"
arch=('x86_64')
license=('MPL2')
depends=('gcc-libs')
makedepends=('cargo')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/rust-lang/mdBook/archive/v${pkgver}.tar.gz")
sha256sums=('a4c9942497b834be6b34d7b532da76384b0f241ebf357c970f350e008e42d368')
# https://github.com/rust-lang/mdBook/blob/master/CHANGELOG.md

prepare() {
  cd "mdBook-${pkgver}"
  mkdir completions/
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "mdBook-${pkgver}"
  cargo build --frozen --release
  "./target/release/$pkgname" completions bash > "completions/$pkgname.bash"
  "./target/release/$pkgname" completions fish > "completions/$pkgname.fish"
  "./target/release/$pkgname" completions zsh > "completions/_$pkgname"
}

check() {
  cd "mdBook-${pkgver}"
  cargo test --frozen
}

package() {
  cd "mdBook-${pkgver}"
  install -Dm 755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
}
