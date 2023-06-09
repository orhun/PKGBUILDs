# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Matteo Giordano <mail at matteogiordano dot me>
# Contributor: qubidt <qubidt at gmail dot com>

pkgname=sniffnet
pkgver=1.2.1
pkgrel=1
pkgdesc="Application to comfortably monitor your network traffic"
arch=('x86_64')
url="https://github.com/GyulyVGC/sniffnet"
license=('Apache' 'MIT')
depends=('alsa-lib' 'fontconfig' 'libpcap' 'freetype2' 'glibc')
makedepends=('cargo')
install=$pkgname.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz"
        "${pkgname}.desktop")
sha512sums=('b367117b107786aef6a2b5f6427e6df984a2052f7506420f7259efe5da0e6edef6962ea0323b2c1f63628b58df883a85ba51ad8ec6196af2421615266c84845c'
            '39d23f967ac05579d9bb87f2c5fcf961f760b0cfab1138253bcc8b22fd9964e27bc9ec6c42e8ed49a287ec5443bf352baf8dd4b4d063c2f6aa29c714d38da2a3')
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
	install -Dm 644 "../${pkgname}.desktop" -t "$pkgdir/usr/share/applications"
}

# vim: ts=2 sw=2 et:
