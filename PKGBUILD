# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Mahor Foruzesh <mahor1221 at gmail dot com>

pkgname=rye
_commit=43ee4fce00021b4cc15dfc3fb92a97b9b156a981
pkgver=0.27.0
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
source=("$pkgname::git+$url.git#commit=$_commit")
sha512sums=('SKIP')
options=('!lto')

prepare() {
	cd "$pkgname"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
	cd "$pkgname"
	export OPENSSL_NO_VENDOR=1
	cargo build --frozen --release
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
}

# vim: ts=2 sw=2 et:
