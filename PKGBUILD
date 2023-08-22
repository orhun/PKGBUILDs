# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=dysk
pkgver=2.8.0
pkgrel=1
pkgdesc="Get information on your mounted filesystems"
arch=('x86_64')
url="https://github.com/Canop/dysk"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
replaces=('lfs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('236e076523295ae074f585bf8f9699f1d150efdace76bd0433b97b63a86abc04d95f8c28ca7653f78e56707afcd4433ccf70007250aa333a6f90985ad7ea91b8')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
