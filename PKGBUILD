# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mahor Foruzesh <mahor1221 at gmail dot com>

pkgname=rye
_commit=58523f69f6d6762af152820110e918354eefcfdc
pkgver=0.33.0
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
sha512sums=('808fb89ccc6adf9bdb0c1816df3d49f84f859aa406c21ea788b6cd9a902eccd6d7a4d90e16d5caaff6750900e388be6ede26aa562ebd6fe3a946b6b2bd10ee9a')
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
