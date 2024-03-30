# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Filipe Nascimento <flipee at tuta dot io>
# Contributor: Attenuation <ouyangjun1999@gmail.com>

pkgname=procs
pkgver=0.14.5
pkgrel=3
pkgdesc='A modern replacement for ps written in Rust'
arch=(x86_64)
url="https://github.com/dalance/$pkgname"
license=(MIT)
depends=(gcc-libs # libgcc_s.so
         glibc) # libc.so libm.so
makedepends=(cargo asciidoctor)
_archive="$pkgname-$pkgver"
source=("$url/archive/v$pkgver/$_archive.tar.gz")
sha256sums=('539b88565c775a106063da5cc5148cfdc7e010534f3dbc90cb8f6317d51ca96b')

prepare() {
	cd "$_archive"
	cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
	cd "$_archive"
	cargo build --release --frozen
	"target/release/$pkgname" --gen-completion zsh
	"target/release/$pkgname" --gen-completion bash
	"target/release/$pkgname" --gen-completion fish
	"target/release/$pkgname" --gen-completion elvish
	asciidoctor -b manpage "man/$pkgname.1.adoc"
}

check() {
	cd "$_archive"
	cargo test --frozen
}

package() {
	cd "$_archive"
	install -Dm0755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
	install -Dm0644 -t "$pkgdir/usr/share/zsh/site-functions/" "_$pkgname"
	install -Dm0644 "$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
	install -Dm0644 -t "$pkgdir/usr/share/fish/vendor_completions.d/" "$pkgname.fish"
	install -Dm0644 -t "$pkgdir/usr/share/elvish/lib/" "$pkgname.elv"
	install -Dm0644 -t "$pkgdir/usr/share/man/man1/" "man/$pkgname.1"
}
