# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Stephen Gregoratto <dev@sgregoratto.me>
# Contributor: Ossama Hjaji <ossama-hjaji@live.fr>

pkgname=onefetch
_commit=24878137250919d4acbebb810dcb5f164d948e17
pkgver=2.20.0
pkgrel=1
pkgdesc="Git repository summary on your terminal"
url="https://github.com/o2sh/onefetch"
license=('MIT')
arch=('x86_64')
makedepends=('cargo' 'git' 'cmake')
checkdepends=('git')
source=("$pkgname::git+$url.git#commit=$_commit")
sha512sums=('SKIP')

prepare() {
  cd "$pkgname"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir -p completions
}

build() {
  cd "$pkgname"
  CFLAGS+=' -ffat-lto-objects'
  cargo build --frozen --release --all-features
  local _completion="target/release/$pkgname --generate"
  $_completion bash > "completions/$pkgbase"
  $_completion fish > "completions/$pkgbase.fish"
  $_completion zsh  > "completions/_$pkgbase"
}

check() {
  cd "$pkgname"
  cargo test --frozen --all-features -- --skip "info::tests::test_style_subtitle"
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "docs/$pkgname.1" "$pkgdir/usr/share/man/man1/$pkgname.1"
  install -Dm 664 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 664 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 664 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
