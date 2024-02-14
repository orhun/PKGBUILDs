# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=lychee
pkgver=0.14.3
pkgrel=2
pkgdesc='Fast, async, resource-friendly link checker written in Rust'
arch=('x86_64')
url=https://lychee.cli.rs
license=('Apache-2.0' 'MIT')
depends=('gcc-libs' 'openssl')
makedepends=('rust')
checkdepends=('cargo-nextest')
conflicts=('lychee-link-checker' 'lychee-rs')
replaces=('lychee-link-checker' 'lychee-rs')
options=('!lto')
source=("$pkgname-$pkgver.tar.gz::https://github.com/lycheeverse/lychee/archive/v$pkgver/$pkgname-$pkgver.tar.gz"
        "fix-ssl-certificate-tests.patch")
b2sums=('9e3ca4c6a1c4ca324185384886a7790d91c4f700bee971f039fc98d5c6dc11e9bb1679a866164153bf1dc8ffcc9e61e7cc7520b79a3bdca894ae4950cf27910c'
        'cfa85d9bd9b344a4a51ff54230f19b0196436ba82e3febff85f8b72b79934dfea01e65303dbf796483b4ddaec855623ac68a6e6e3b47aa010137fe87ad176d73')

prepare() {
  cd $pkgname-$pkgver
  patch -Np1 -i "$srcdir/fix-ssl-certificate-tests.patch"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
}

check() {
  cd $pkgname-$pkgver
  # Avoid vendoring openssl, which is enabled by vendored-openssl feature
  export OPENSSL_NO_VENDOR=1
  cargo nextest run --all-targets --all-features --filter-expr '!test(test_exclude_example_domains)' --test-threads 1
  cargo nextest run --filter-expr 'test(test_exclude_example_domains)' --test-threads 1
  cargo test --doc
}

package() {
  cd $pkgname-$pkgver
  install -Dt "$pkgdir"/usr/bin target/release/$pkgname
  install -Dm644 -t "$pkgdir"/usr/share/doc/$pkgname README.md
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname LICENSE-MIT
}
