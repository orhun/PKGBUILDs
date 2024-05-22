# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mahor Foruzesh <mahor1221 at gmail dot com>

pkgname=rye
_commit=d31340178df9b1cf97ea96b6856f2b13383bed8f
pkgver=0.34.0
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
sha512sums=('186208ae0e6ffdc91090dac5741ecbfc0fade1ef1ddc0c1e4de9068c3db2de5980ef923d81513fac7930a0a44a7e976b7a4f306a709da890381a673e85dbab39')
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
