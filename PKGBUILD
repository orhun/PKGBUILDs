# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=dysk
pkgver=2.8.2
pkgrel=1
pkgdesc="Get information on your mounted filesystems"
arch=('x86_64')
url="https://github.com/Canop/dysk"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
replaces=('lfs')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('1fe771a5c74cc75d3742bca8f3d69fc386be0d015ab16205f95c38bf669131ca2129c8bf461db5d1cbad6783f869953b8803faa6b9d32d12fbb7fabd7f0fdde5')

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
