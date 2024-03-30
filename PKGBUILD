# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mahor Foruzesh <mahor1221 at gmail dot com>

pkgname=rye
_commit=e1b4f2a290950652d75412db22e9b6370ceb3fef
pkgver=0.32.0
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
source=("$pkgname::git+$url.git#commit=$_commit"
        "cargo-lock.patch")
sha512sums=('92465cf45a42745771bda8b5274536f2f9ea3f8b100423dc906aa5c87abf3c009caa7cfc0ab95cf6c67840f0a22d2d20db16c9b093f38fb578d77896e1d8ca00'
            'c4f61eec42614aed89a4d70ed7cdfeb6e11a78598f372d8614fb8a1f098850daa6405dc1de5bcc8329d6a0958e4ca55f9a1e3d829e5f7b2b964c252744a32bd1')
options=('!lto')

prepare() {
	cd "$pkgname"
	patch -Np1 -i "$srcdir/cargo-lock.patch"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	mkdir completions
}

build() {
	cd "$pkgname"
	export OPENSSL_NO_VENDOR=1
	cargo build --frozen --release
	local compgen="target/release/$pkgname self completion -s"
	$compgen bash >"completions/$pkgbase"
	$compgen elvish >"completions/$pkgbase.elv"
	$compgen fish >"completions/$pkgbase.fish"
	$compgen zsh >"completions/_$pkgbase"
}

check() {
	cd "$pkgname"
	export OPENSSL_NO_VENDOR=1
	cargo test --frozen
}

package() {
	cd "$pkgname"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
	install -Dm 644 "completions/$pkgname.elv" -t "$pkgdir/usr/share/elvish/lib/"
	install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
	install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
