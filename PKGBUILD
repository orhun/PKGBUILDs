# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=flawz
pkgver=0.2.1
pkgrel=1
pkgdesc="A Terminal UI for browsing security vulnerabilities (CVEs)"
arch=('x86_64')
url="https://github.com/orhun/flawz"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'openssl' 'sqlite')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('4bfdde3494de5e9954cf8ac85589794dc298dd41890fee4984bc388a75c3f861b7baa66eeb61a018ab172de97fc25e3db45ee2bf7de3a8b90eca1f6302b9e300')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions/
  mkdir man/
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  OUT_DIR=completions/ "./target/release/$pkgname-completions"
  OUT_DIR=man/ "./target/release/$pkgname-mangen"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
