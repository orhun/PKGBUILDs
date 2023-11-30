# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cocogitto
_pkgname=cog
pkgver=6.0.0
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
sha256sums=('090283fe3d7ac574e87bb5ef5dedecdcc3745f25cf82353b3cc2fa9e15cf53aa')

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
