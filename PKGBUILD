# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=spicy-launcher
pkgver=0.3.1
pkgrel=1
pkgdesc="The launcher for Spicy Lobster games"
arch=('x86_64')
url="https://github.com/spicylobstergames/SpicyLauncher"
license=('MIT' 'Apache')
depends=('pkg-config' 'mesa-libgl' 'alsa-lib' 'systemd-libs' 'libudev.so' 'gtk3' 'libsoup' 'webkit2gtk')
makedepends=('cargo' 'yarn' 'npm')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('b1e9db094471b7a4d3e3a645faf5b9ed1240a7bf98d03c3cb39ebe04d6fa0b81fc4d046c85cebcc4952119e3d4186692f67902539faa27e075d89ea8dad0bc9c')
options=('!lto')

prepare() {
	cd "SpicyLauncher-$pkgver"
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
	cd "SpicyLauncher-$pkgver/gui"
	yarn install --ignore-engines
	yarn tauri build --target "$CARCH-unknown-linux-gnu" --bundles none
	cd ..
	cargo build --release --frozen
}

package() {
	cd "SpicyLauncher-$pkgver"
	install -Dm 755 "target/release/$pkgname-cli" -t "$pkgdir/usr/bin"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
