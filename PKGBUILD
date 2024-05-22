# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kxxt <rsworktech at outlook dot com>

pkgname=tracexec
pkgver=0.3.1
pkgrel=1
pkgdesc="A small utility for tracing execve{,at} and pre-exec behavior"
arch=('x86_64')
url="https://github.com/kxxt/tracexec"
license=('GPL-2.0-or-later')
depends=('gcc-libs')
makedepends=('cargo' 'cargo-about' 'git')
source=("$pkgname-$pkgver::git+https://github.com/kxxt/tracexec.git#tag=v$pkgver")
b2sums=('e451e2fd838964aed48b1c18e263c5e1a97cf29ee3f3bd2fd6edf0cd467157d0d855c2f293e458ffb382dae7c071c8279c000d4e7bca75325d796c333536e12d')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions/
}

build() {
  cd "$pkgname-$pkgver"
  # --bins: needed for test
  cargo build --bins --frozen --release --all-features
  cargo about generate -o THIRD_PARTY_LICENSES.HTML about.hbs
  local compgen="target/release/$pkgname generate-completions"
  $compgen bash >"completions/$pkgbase"
  $compgen elvish >"completions/$pkgbase.elv"
  $compgen fish >"completions/$pkgbase.fish"
  $compgen zsh >"completions/_$pkgbase"
}

check() {
  cd "$pkgname-$pkgver"
  RUST_TEST_THREADS=1 cargo test --frozen --release --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
  install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 THIRD_PARTY_LICENSES.HTML "$pkgdir/usr/share/licenses/$pkgname/THIRD_PARTY_LICENSES.HTML"
  install -Dm644 "completions/$pkgbase" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm644 "completions/$pkgbase.elv" -t "$pkgdir/usr/share/elvish/lib/"
  install -Dm644 "completions/$pkgbase.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm644 "completions/_$pkgbase" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim:set ts=2 sw=2 et:
