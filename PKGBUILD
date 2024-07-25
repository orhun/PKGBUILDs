# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Stijn Seghers <stijnseghers at gmail dot com>

pkgname=cargo-shuttle
_commit=e2e178cf0b98c75a005382fc29535abaebe771ba
pkgver=0.47.0
pkgrel=1
pkgdesc='Cargo command for the shuttle platform'
arch=('x86_64')
url="https://github.com/shuttle-hq/shuttle"
license=('Apache-2.0')
depends=('cargo' 'gcc-libs' 'zlib' 'curl')
makedepends=('git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "$pkgname-examples::git+https://github.com/shuttle-hq/examples.git")
sha512sums=('de04d0e3246e58795d25b435276fb41273a2a2251b1945d27bf096f402eb7517ee4804c67ab022ffd700265620681484a748c30a17195468759df5cb9f05602d'
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
