# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-llvm-cov
pkgver=0.6.11
pkgrel=1
pkgdesc="Cargo subcommand to easily use LLVM source-based code coverage (-Z instrument-coverage)."
arch=('x86_64')
url="https://github.com/taiki-e/cargo-llvm-cov"
license=('MIT' 'Apache-2.0')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('92f7abd853a6e2968390ab48fa38268352aff076a0f0c441b34244aee34054de'
            '860299dff1dd3a4b7b9661e79f540892fa2317ac519e901ab0e61ce9808a989c')

prepare() {
  cd "$pkgname-$pkgver"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
