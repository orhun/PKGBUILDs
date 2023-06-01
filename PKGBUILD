# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=release-plz
pkgver=0.3.11
pkgrel=1
pkgdesc="Release Rust packages without using the command line"
arch=('x86_64')
url="https://github.com/MarcoIeni/release-plz"
license=('MIT' 'Apache')
depends=('gcc-libs' 'curl')
checkdepends=('git')
makedepends=('cargo')
optdepends=('cargo-semver-checks: check for API breaking changes')
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgname-v$pkgver.tar.gz")
sha512sums=('c7dedfc316f473803a7244baae37be119b73a60ff4765c8b2253a7b56a32eb874ee0f164529fa37a51fb652972895881f04d72eb1c90cb9b53d8bfb2659b4cda')
options=('!lto')

prepare() {
	mv "$pkgname-$pkgname-v$pkgver" "$pkgname-$pkgver"
	cd "$pkgname-$pkgver"
	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
	mkdir completions
}

build() {
	cd "$pkgname-$pkgver"
	cargo build --release --frozen
	local compgen="target/release/$pkgname generate-completions"
	$compgen bash >"completions/$pkgname"
	$compgen fish >"completions/$pkgname.fish"
	$compgen zsh >"completions/_$pkgname"
}

check() {
	cd "$pkgname-$pkgver"
	cargo test --frozen
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
