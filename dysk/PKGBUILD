# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=dysk
pkgver=2.9.0
pkgrel=1
pkgdesc="Get information on your mounted filesystems"
arch=('x86_64')
url="https://github.com/Canop/dysk"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
replaces=('lfs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('d623c7312c1b93b4fa137e5ab599f4fdc406cfeaf13ba5ac10d1e08e010d2d327bb38b19f887aa501d212e0083b0c8c8c747f25e3db3ce832a52ca4e9502543b')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  out_dir=$(find target -type f -name "$pkgname.bash" -exec dirname {} \;)
  install -Dm 644 "$out_dir/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "$out_dir/$pkgname.fish" "$pkgdir/usr/share/fish/vendor_completions.d/$pkgname.fish"
  install -Dm 644 "$out_dir/_$pkgname" "$pkgdir/usr/share/zsh/site-functions/_$pkgname"
  install -Dm 644 "$out_dir/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim: ts=2 sw=2 et:
