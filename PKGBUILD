# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Evan McCarthy <evanmccarthy@outlook.com>
# Contributor: Oleksandr Natalenko <oleksandr@natalenko.name>

pkgname=tere
pkgver=1.5.1
pkgrel=1
pkgdesc="A terminal file explorer"
arch=('x86_64')
url="https://github.com/mgunyho/tere"
license=("custom:EUPL")
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('d7f657371ffbd469c4d8855c2a2734c20b53ae632fe3cbf9bb7cab94bd726326')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

	cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
	cd "$srcdir/$pkgname-$pkgver"

	cargo build --release --frozen
}

check() {
	cd "$srcdir/$pkgname-$pkgver"

  # https://github.com/mgunyho/tere/issues/93
	cargo test --frozen -- \
	  --skip "first_run_prompt_accept" \
	  --skip "output_on_exit_without_cd" \
	  --skip "first_run_prompt_cancel" \
	  --skip "basic_run"
}

package() {
	cd ${pkgname}-${pkgver}

	install -Dt "${pkgdir}"/usr/bin -m0755 target/release/${pkgname}
	install -Dt "${pkgdir}"/usr/share/licenses/${pkgname} -m0644 LICENSE
	install -Dt "${pkgdir}"/usr/share/doc/${pkgname} -m0644 README.md
	install -Dt "${pkgdir}"/usr/share/doc/${pkgname}/demo -m0644 demo/*
}

# vim:set ts=2 sw=2 et:
