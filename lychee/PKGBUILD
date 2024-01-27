# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=lychee
pkgver=0.14.2
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
source=("$pkgname-$pkgver.tar.gz::https://github.com/lycheeverse/lychee/archive/v$pkgver/$pkgname-$pkgver.tar.gz"
        "$pkgname-$pkgver-fix-tests.patch::https://github.com/lycheeverse/lychee/commit/351e433abc2516b597496f54a668daa4bade6121.patch")
b2sums=('862e542d482633117725fc4dd9a7387df2560fe689d83026211e0f309724bd4364ae995e6f11747590d54bc348f4be4d440fa8fa14a58d71bd1d27149d9d7854'
        '369409ae656ebc59f05832adaa8cd092a79f0594973734142e4050b5fd9f2651e8c63b42e41fb9b0ef0bb750b6a7cf6232c3d37aefcc6b435479e756286a8a3f')

prepare() {
  cd $pkgname-$pkgver
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  patch -Np1 -i "$srcdir/$pkgname-$pkgver-fix-tests.patch"
}

build() {
  cd $pkgname-$pkgver
  cargo build --release --frozen
}

check() {
  cd $pkgname-$pkgver
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
