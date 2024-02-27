# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=git-cliff
pkgver=2.0.4
pkgrel=2
pkgdesc="A highly customizable changelog generator"
arch=('x86_64')
url="https://github.com/orhun/git-cliff"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'zlib' 'libgit2.so')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('60ab79faab4968412d7aba1dddfc156fb1365254e06d8a4f6c9b90ed1ad3ba5161588675c4864b9577695ca42ae8044725300da35f90b5c9024ced2c326ddf50')

prepare() {
  cd "$pkgname-$pkgver"
  mkdir completions/
  mkdir man/
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
  cargo build --release --frozen --no-default-features --features github
  OUT_DIR=completions/ "./target/release/$pkgname-completions"
  OUT_DIR=man/ "./target/release/$pkgname-mangen"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- --skip "git_log" --skip "git_tags" --skip "git_upstream_remote"
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
