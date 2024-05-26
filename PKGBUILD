# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: kxxt <rsworktech at outlook dot com>

pkgname=tracexec
pkgver=0.4.0
pkgrel=1
pkgdesc="A small utility for tracing execve{,at} and pre-exec behavior"
arch=('x86_64')
url="https://github.com/kxxt/tracexec"
license=('GPL-2.0-or-later')
depends=('gcc-libs')
makedepends=('cargo' 'cargo-about' 'git')
source=("$pkgname-$pkgver::git+https://github.com/kxxt/tracexec.git#tag=v$pkgver")
b2sums=('afb62345eae21053bd4f18767319242cc58bda00880d44783ff422e7b59d9af7f5c8ab1ac89f3817323569ee922611d3a9ded0248a11be2a658965fbec610b6d')

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
