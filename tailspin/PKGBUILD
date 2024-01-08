# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Justin ! <just1602@riseup.net>

pkgname=tailspin
pkgver=2.3.0
pkgrel=1
pkgdesc='A log file highlighter'
url="https://github.com/bensadeh/$pkgname"
arch=(x86_64 aarch64 arm armv7h armv6h)
license=(MIT)
makedepends=(cargo)
_archive="$pkgname-$pkgver"
source=("$url/archive/$pkgver/$_archive.tar.gz")
sha256sums=('f523a9ccf59e6d5ae4bb66a5b0a4d480832f604c09a3c2f4dd00b5efc8f1b03d')

prepare() {
	cd "$_archive"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
	mv completions/{tspin.zsh,_tspin}
	mv completions/{tspin.bash,tspin}
}

build() {
	cd "$_archive"
	cargo build --frozen --release
}

check() {
	cd "$_archive"
	cargo test --frozen
}

package() {
	cd "$_archive"
	install -Dm755 -t "$pkgdir/usr/bin/" target/release/tspin
	install -Dm644 -t "$pkgdir/usr/share/man/man1/" man/tspin.1
	install -Dm644 -t "$pkgdir/usr/share/bash-completion/completions/" completions/tspin
	install -Dm644 -t "$pkgdir/usr/share/zsh/site-functions/" completions/_tspin
	install -Dm644 -t "$pkgdir/usr/share/fish/vendor_completions.d/" completions/tspin.fish
	install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENCE
}
