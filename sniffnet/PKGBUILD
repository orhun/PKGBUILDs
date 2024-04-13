# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Matteo Giordano <mail at matteogiordano dot me>
# Contributor: qubidt <qubidt at gmail dot com>

pkgname=sniffnet
pkgver=1.3.0
pkgrel=2
pkgdesc="Application to comfortably monitor your network traffic"
arch=('x86_64')
url="https://github.com/GyulyVGC/sniffnet"
license=('Apache-2.0' 'MIT')
depends=('alsa-lib' 'fontconfig' 'libpcap' 'freetype2' 'glibc' 'zenity' 'xdg-desktop-portal')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha512sums=('671900e75551770e96bcc3f7440911696d71f0972e64eae30ea42951a7376e0a439d68d1426c4c8fcde9e61ccd30e3f29e3a603f58db147115a07293a5206610')
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
