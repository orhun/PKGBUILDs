# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Stijn Seghers <stijnseghers at gmail dot com>

pkgname=cargo-shuttle
_commit=299a30db5b3361c328b3231971d8276d10995be7
pkgver=0.33.0
pkgrel=1
pkgdesc='Cargo command for the shuttle platform'
arch=('x86_64')
url="https://github.com/shuttle-hq/shuttle"
license=('Apache')
depends=('gcc-libs' 'zlib' 'curl')
makedepends=('cargo' 'git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "$pkgname-examples::git+https://github.com/shuttle-hq/examples.git")
sha512sums=('SKIP'
            'SKIP')
options=('!lto')

prepare() {
  cd "$pkgname"
  git submodule init
  git config submodule."examples".url "${srcdir}/${pkgname}"-examples
  git -c protocol.file.allow=always submodule update --init --recursive
  mkdir completions

  cd "$pkgname"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname/$pkgname"
  cargo build --release --frozen
  cd ..
  local compgen="target/release/$pkgname generate -s"
  $compgen bash >"completions/$pkgname"
  $compgen fish >"completions/$pkgname.fish"
  $compgen zsh >"completions/_$pkgname"
}

check() {
  cd "$pkgname/$pkgname"
  cargo test --frozen --lib
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 "$pkgname/README.md" -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim:set ts=2 sw=2 et:
