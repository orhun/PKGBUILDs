# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=release-plz
pkgver=0.3.49
pkgrel=1
_commit=93d1e72a89d34cb07f8f0a656155d71f2511e5d4
pkgdesc="Release Rust packages without using the command line"
arch=('x86_64')
url="https://github.com/MarcoIeni/release-plz"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'curl' 'libgit2' 'openssl')
makedepends=('cargo' 'git')
optdepends=('cargo-semver-checks: check for API breaking changes')
source=("$pkgname::git+$url.git#commit=$_commit")
sha512sums=('SKIP')
options=('!lto')

prepare() {
	cd "$pkgname"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	mkdir completions
}

build() {
	cd "$pkgname"
	cargo build --release --frozen --no-default-features
	local compgen="target/release/$pkgname generate-completions"
	$compgen bash >"completions/$pkgname"
	$compgen fish >"completions/$pkgname.fish"
	$compgen zsh >"completions/_$pkgname"
}

check() {
	cd "$pkgname"
	cargo test --frozen --no-default-features -- --skip "next_ver"
}

package() {
	cd "$pkgname"
	install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
	install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
	install -Dm 644 "completions/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
	install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
	install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}

# vim: ts=2 sw=2 et:
