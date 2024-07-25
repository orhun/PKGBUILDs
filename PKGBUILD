# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=release-plz
pkgver=0.3.79
pkgrel=1
_commit=a9fcca836b0388bcaa67478ecc3ecb35a2d443d0
pkgdesc="Release Rust packages without using the command line"
arch=('x86_64')
url="https://github.com/MarcoIeni/release-plz"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'curl' 'libgit2' 'openssl')
makedepends=('cargo' 'git')
optdepends=('cargo-semver-checks: check for API breaking changes')
source=("$pkgname-$pkgver::git+$url.git#commit=$_commit")
sha512sums=('d896a70856582c7d44cff3ee4620455c8228bde9faab403b7df4482f2aa536b4b630ee939f417e7c8db2f812ec51b8d5e0ebf72bedd21a7c10249f6490aded15')
options=('!lto')

prepare() {
	cd "$pkgname-$pkgver"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	mkdir completions
}

build() {
	cd "$pkgname-$pkgver"
	cargo build --release --frozen --no-default-features
	local compgen="target/release/$pkgname generate-completions"
	$compgen bash >"completions/$pkgname"
	$compgen fish >"completions/$pkgname.fish"
	$compgen zsh >"completions/_$pkgname"
}

check() {
	cd "$pkgname-$pkgver"
	cargo test --frozen --no-default-features -- --skip "next_ver"
}

package() {
	cd "$pkgname-$pkgver"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
	install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
	install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
