# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>

pkgbase=kondo
pkgname=(kondo kondo-ui)
pkgver=0.8
pkgrel=1
pkgdesc='Save disk space by cleaning non-essential files from software projects'
arch=('x86_64')
url='https://github.com/tbillington/kondo'
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'pango' 'gdk-pixbuf2' 'gtk3')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "$pkgname-$pkgver-cargo-lock.patch::$url/commit/249db58bf90b9603fd903879ebff8ba94d47c3cf.patch")
sha512sums=('62cf51c7db440fa36d33206759a60b084a1c98fc718988cfa01c417ad1eb4e6a930e3c66e83d2ae9fc169acb93c98ed18fe8cf4ca3ab5a40d2adbfa27363f9a0'
            'ba045232153b80fb177ad26d4d6b298f7043ee729f01a0cb3cb8c80ebed4434d5b71761678f77ba2b8a7e523e8ea2bc3434ef5f6f258f36e6b15c37833fe64d1')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"
	patch -Np1 -i "$srcdir/$pkgname-$pkgver-cargo-lock.patch"

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
