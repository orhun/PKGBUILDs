# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cocogitto
_pkgname=cog
pkgver=5.5.0
pkgrel=1
pkgdesc='Set of CLI tools for the conventional commit and semver specifications'
arch=(x86_64)
url="https://github.com/$pkgname/$pkgname"
license=(MIT)
depends=(git
         gcc-libs
         libgit2.so
         zlib)
makedepends=(cargo)
_archive="$pkgname-$pkgver"
source=("$url/archive/$pkgver/$_archive.tar.gz")
sha256sums=('709c54c6c64463af607590ac970dc5a45cbcc0236a5a15d609d9a77461f11325')

prepare() {
	cd "$_archive"
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
	mkdir {completions,man}
}

build() {
	cd "$_archive"
	CFLAGS+=" -ffat-lto-objects"
	cargo build --frozen --release
	local compgen="target/release/$_pkgname generate-completions"
	local mangen="target/release/$_pkgname generate-manpages"
	$compgen bash > "completions/$_pkgname"
	$compgen fish > "completions/$_pkgname.fish"
	$compgen zsh  > "completions/_$_pkgname"
	$mangen man/
}

check() {
	cd "$_archive"
	# Test suite is not atomic, relies on user environment such as git user configs
	# cargo test --frozen
}

package() {
	cd "$_archive"
	install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$_pkgname"
	install -Dm0644 -t "$pkgdir/usr/share/bash-completion/completions/" "completions/$_pkgname"
	install -Dm0644 -t "$pkgdir/usr/share/fish/vendor_completions.d/" "completions/$_pkgname.fish"
	install -Dm0644 -t "$pkgdir/usr/share/zsh/site-functions/" "completions/_$_pkgname"
	install -Dm0644 -t "$pkgdir/usr/share/doc/$pkgname/" README.md
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
	install -Dm0644 -t "$pkgdir/usr/share/man/man1" man/*.1
}
