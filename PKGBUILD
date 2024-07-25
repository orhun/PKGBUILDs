# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mahor Foruzesh <mahor1221 at gmail dot com>

pkgname=rye
_commit=09b67c469d92acb6d31d561176c7f43e2947ea62
pkgver=0.37.0
pkgrel=1
pkgdesc="An experimental alternative to poetry, pip, pipenv, venv, virtualenv, pdm, hatch"
arch=('x86_64')
url="https://github.com/astral-sh/rye"
license=('MIT')
depends=(
	zlib
	bzip2
	openssl
	gcc-libs
	libxcrypt-compat
)
makedepends=('cargo' 'git')
source=("$pkgname-$pkgver::git+$url.git#commit=$_commit")
sha512sums=('c75ac26b5cd3944194d7421ae5661e600789e3b94f2645f2fca5437e746ef3d45cb7e4c83ca9699467ab125a3509938d40a3def9fdb1134208bdaa9881955e92')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	mkdir completions
}

build() {
	cd "$pkgname-$pkgver"
	export OPENSSL_NO_VENDOR=1
	cargo build --frozen --release
	local compgen="target/release/$pkgname self completion -s"
	$compgen bash >"completions/$pkgbase"
	$compgen elvish >"completions/$pkgbase.elv"
	$compgen fish >"completions/$pkgbase.fish"
	$compgen zsh >"completions/_$pkgbase"
}

check() {
	cd "$pkgname-$pkgver"
	export OPENSSL_NO_VENDOR=1
	cargo test --frozen
}

package() {
	cd "$pkgname-$pkgver"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
	install -Dm 644 "completions/$pkgname.elv" -t "$pkgdir/usr/share/elvish/lib/"
	install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
	install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
