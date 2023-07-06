# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>

pkgbase=kondo
pkgname=(kondo kondo-ui)
pkgver=0.7
pkgrel=1
pkgdesc='Save disk space by cleaning non-essential files from software projects'
arch=('x86_64')
url='https://github.com/tbillington/kondo'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'pango' 'gdk-pixbuf2' 'gtk3')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('21a795ce2b61286aa6b1828dd2b6924b42f84881bd5d7b0bdb9b29016203d404b577a245cacd688cbf57acb7c2d9208fd9be849ea19a14662a5ef15d0fdecf86')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"

	# download dependencies
	_opts="--locked --target $CARCH-unknown-linux-gnu"
	cargo fetch $_opts
	cargo fetch $_opts --manifest-path "$pkgname-ui/Cargo.toml"
}

build() {
	cd "$pkgname-$pkgver"

	_opts="--frozen --release"
	cargo build $_opts
	cargo build $_opts --manifest-path "$pkgname-ui/Cargo.toml"
}

package_kondo() {
	cd "$pkgname-$pkgver"

	# binary
	install -vDm755 -t "$pkgdir/usr/bin" "target/release/$pkgname"

	# documentation
	install -vDm644 -t "$pkgdir/usr/share/doc/$pkgname" README.md

	# license
	install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE
}

package_kondo-ui() {
	pkgdesc='Save disk space by cleaning non-essential files from software projects (UI)'
	depends+=('glib2' 'cairo' 'gtk3')
	cd "${pkgname%-ui}-$pkgver"

	# binary
	install -vDm755 -t "$pkgdir/usr/bin" "$pkgname/target/release/$pkgname"

	# documentation
	install -vDm644 -t "$pkgdir/usr/share/doc/$pkgname" README.md

	# license
	install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE
}

# vim: ts=2 sw=2 et:
