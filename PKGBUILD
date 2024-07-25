# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Matteo Giordano <mail at matteogiordano dot me>
# Contributor: qubidt <qubidt at gmail dot com>

pkgname=sniffnet
pkgver=1.3.1
pkgrel=1
pkgdesc="Application to comfortably monitor your network traffic"
arch=('x86_64')
url="https://github.com/GyulyVGC/sniffnet"
license=('Apache-2.0' 'MIT')
depends=('alsa-lib' 'fontconfig' 'libpcap' 'freetype2' 'glibc' 'zenity' 'xdg-desktop-portal')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha512sums=('99a7267bed9a0cf35cc868c214d36aa9f75b12146c8d9b4964fe32f3747ee3f712fb51764601d56adeb4058556c3c2f0e8714e282fe03ad058bb2f3124519ae9')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
	cd "$pkgname-$pkgver"
	cargo build --frozen --release
}

check() {
	cd "$pkgname-$pkgver"
	cargo test --frozen
}

package() {
	cd "$pkgname-$pkgver"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm 644 "resources/logos/raw/icon.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
	install -Dm 644 "resources/packaging/linux/${pkgname}.desktop" -t "$pkgdir/usr/share/applications"
}

# vim: ts=2 sw=2 et:
