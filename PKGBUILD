# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

pkgname=lychee
pkgver=0.14.1
pkgrel=1
pkgdesc='Fast, async, resource-friendly link checker written in Rust'
arch=('x86_64')
url=https://lychee.cli.rs
license=('Apache' 'MIT')
depends=('gcc-libs' 'openssl')
makedepends=('rust')
checkdepends=('cargo-nextest')
conflicts=('lychee-link-checker' 'lychee-rs')
replaces=('lychee-link-checker' 'lychee-rs')
options=('!lto')
source=("$pkgname-$pkgver.tar.gz::https://github.com/lycheeverse/lychee/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
b2sums=('d61651040593f46a2bc2f538742417b883db1294dcdfc4ecca92ae5a03e8e4343aa2bdf7fd3e9976af465805fdea63044cd789f32d1c0f7a5cb4fc93225af096')

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
