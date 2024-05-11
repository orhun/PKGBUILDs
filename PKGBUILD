# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=git-cliff
pkgver=2.2.2
pkgrel=1
pkgdesc="A highly customizable changelog generator"
arch=('x86_64')
url="https://github.com/orhun/git-cliff"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'glibc' 'zlib' 'libgit2')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('f9b21fe188a7bf729e82d4b1828649e938f10eaaee5a164963a8a109fdeaeb5f6148fe0e8cadf0c59e4cfb18759eb7a2c74cb4c7a7a84a2d730c1f9a2eb97f41')

prepare() {
  cd "$pkgname-$pkgver"
  mkdir -p completions/
  mkdir -p man/
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=' -ffat-lto-objects'
  cargo build --release --frozen --no-default-features --features github
  OUT_DIR=completions/ "./target/release/$pkgname-completions"
  OUT_DIR=man/ "./target/release/$pkgname-mangen"
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- --skip "repo::test"
}

package() {
  depends+=(libgit2.so libz.so)
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
