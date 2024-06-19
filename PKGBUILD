# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: replydev <commoncargo@tutanota.com>

pkgbase=cotp
pkgname=(cotp cotp-converters)
pkgver=1.7.1
pkgrel=1
pkgdesc='Trustworthy, encrypted, command-line TOTP/HOTP authenticator app with import functionality'
arch=(x86_64)
url="https://github.com/replydev/$pkgname"
license=(GPL-3.0-only)
makedepends=(cargo
             python)
optdepends=('cotp-converters: additional scripts import from other OTP apps')
replaces=("$pkgname-bin")
_archive="$pkgname-$pkgver"
source=("$url/archive/v$pkgver/$_archive.tar.gz")
sha256sums=('62c7bd4b5f3435cc04add28041a896ea76605c0c0675e711672b2dc2221cbccf')

prepare(){
	cd "$_archive"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
	cd "$_archive"
	cargo build --frozen --release --all-features
}

check() {
	cd "$_archive"
	cargo test --frozen --all-features
}

package_cotp() {
	cd "$_archive"
	depends+=(gcc-libs # libgcc_s.so
	          glibc # libc.so libm.so
	          libxcb
	          libxkbcommon-x11)
	install -Dm0755 -t "$pkgdir/usr/bin/" "target/release/$pkgname"
}

package_cotp-converters() {
	cd "$_archive"
	depends+=(cotp
	          python)
	install -Dm0755 -t "$pkgdir/usr/share/cotp/converters/" converters/*.py
}
