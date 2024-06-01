# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-llvm-cov
pkgver=0.6.10
pkgrel=1
pkgdesc="Cargo subcommand to easily use LLVM source-based code coverage (-Z instrument-coverage)."
arch=('x86_64')
url="https://github.com/taiki-e/cargo-llvm-cov"
license=('MIT' 'Apache-2.0')
depends=('cargo' 'gcc-libs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "Cargo.lock")
sha256sums=('b8250ee10a3902b20c5c93b3ddd37e98a375048e9c7d500c5dafc950c3790415'
            '9a59af33fec54248528cbb6e78426a654dc3f3a94bf0a7f51055e2635f9bfcea')

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
