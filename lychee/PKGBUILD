# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=lychee
pkgver=0.15.1
pkgrel=1
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
source=("$pkgname-$pkgver.tar.gz::https://github.com/lycheeverse/lychee/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
b2sums=('5d9895468dd6ab10ffc37e9a341bec96f3a927e9be246d58f6dbb9e63e8202bcc4688ccbffd01e90c69229e48cfe473129b800f99ef657c33cf67180d2384067')

prepare() {
  cd $pkgname-$pkgver
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
  test_expr="(!test(test_exclude_example_domains) and !test(test_detailed_json_output_on_error))"
  cargo nextest run --all-targets --all-features -E "$test_expr" --test-threads 1
  cargo nextest run --filter-expr 'test(test_exclude_example_domains)' --test-threads 1
  cargo test --doc
}

package() {
  cd $pkgname-$pkgver
  install -Dt "$pkgdir"/usr/bin target/release/$pkgname
  install -Dm644 -t "$pkgdir"/usr/share/doc/$pkgname README.md
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname LICENSE-MIT
}
