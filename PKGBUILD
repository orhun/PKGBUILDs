# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Wesley Moore <wes@wezm.net>

pkgname=xh
pkgver=0.22.0
pkgrel=1
pkgdesc="Friendly and fast tool for sending HTTP requests"
arch=('x86_64')
url="https://github.com/ducaale/xh"
license=('MIT')
depends=('gcc-libs' 'openssl')
makedepends=('cargo')
replaces=('ht-rs' 'ht')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('72f4d5e24165d8749433167e3ad3df8f26faafb250f1232acbe5192843e4157c')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=' -ffat-lto-objects'
  cargo build --frozen --release --features native-tls
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --features native-tls
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "doc/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
  install -Dm 644 "completions/$pkgname.bash" "${pkgdir}/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "${pkgdir}/usr/share/zsh/site-functions"
  # `xh` will default to HTTPS scheme if the binary name is one of `xhs`, `https`, or `xhttps`
  ln -s "/usr/bin/$pkgname" "$pkgdir/usr/bin/${pkgname}s"
}

# vim: ts=2 sw=2 et:
