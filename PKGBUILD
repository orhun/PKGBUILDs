# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.28
_commit=f9e88fc116c5735545d5c0b8084bdff9eea7ed04
pkgrel=1
pkgdesc="A cargo subcommand to provide various options useful for testing and CI"
arch=('x86_64')
url="https://github.com/taiki-e/cargo-hack"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo' 'git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "Cargo.lock")
sha512sums=('422bd4552347fba328db229a3157d901452168a15ce1f5b1b118273d920930cf0234dff8b36180609c584557ef53dc1efcf0b98eafa1c84a2c3cd82b5e914b45'
            'c6be4a24bfabf4136c047ed9bead607759c2a75091e75b200679f06c5b19cc1e38ffb507d26d082ba0bd5b3363d8e972e8e1004a99a8955d0926816f18abb20c')

prepare() {
  cd "$pkgname"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname"
  cargo build --release --frozen
}

check() {
  cd "$pkgname"
  cargo test --frozen -- \
    --skip "multi_target" \
    --skip "version_range" \
    --skip "version_range_failure"
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  depends+=(rustup)
}

# vim: ts=2 sw=2 et:
