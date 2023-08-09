# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Matteo Giordano <mail at matteogiordano dot me>
# Contributor: qubidt <qubidt at gmail dot com>

pkgname=sniffnet
pkgver=1.2.2
pkgrel=1
pkgdesc="Application to comfortably monitor your network traffic"
arch=('x86_64')
url="https://github.com/GyulyVGC/sniffnet"
license=('Apache' 'MIT')
depends=('alsa-lib' 'fontconfig' 'libpcap' 'freetype2' 'glibc')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha512sums=('54f766fdea63e00b9156e9b03f55eedc38dbbd5a08b668fc84466cd6b2ba736fb1f570d907503664992ad3d7524bb4b481e100ada4e6198487b2bfed45805c56')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
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
