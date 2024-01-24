# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Stijn Seghers <stijnseghers at gmail dot com>

pkgname=cargo-shuttle
_commit=9c1199c950f24804d23eb8ff631d92d3b289d667
pkgver=0.37.0
pkgrel=1
pkgdesc='Cargo command for the shuttle platform'
arch=('x86_64')
url="https://github.com/shuttle-hq/shuttle"
license=('Apache-2.0')
depends=('cargo' 'gcc-libs' 'zlib' 'curl')
makedepends=('git')
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
  mkdir man

  cd "$pkgname"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname/$pkgname"
  cargo build --release --frozen
  cd ..
  local compgen="target/release/$pkgname generate shell"
  $compgen bash >"completions/$pkgname"
  $compgen fish >"completions/$pkgname.fish"
  $compgen zsh >"completions/_$pkgname"
  "target/release/$pkgname" generate manpage > "man/$pkgname.1"
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
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim:set ts=2 sw=2 et:
