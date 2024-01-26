# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: cauebs <cauebs@pm.me>
# Contributor: cyqsimon <669-cyqsimon@users.noreply.gitlab.archlinux.org>

pkgname=hyperfine
pkgver=1.18.0
pkgrel=2
pkgdesc="A command-line benchmarking tool"
url="https://github.com/sharkdp/hyperfine"
arch=("x86_64")
license=("APACHE" "MIT")
depends=(gcc-libs)
makedepends=(cargo)
optdepends=('python-numpy: run data analysis scripts'
            'python-matplotlib: run data analysis scripts'
            'python-scipy: run data analysis scripts')
source=("$pkgname-$pkgver.tar.gz::https://github.com/sharkdp/$pkgname/archive/v$pkgver.tar.gz")
options=(zipman)
sha256sums=('fea7b92922117ed04b9c84bb9998026264346768804f66baa40743c5528bed6b')

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
  cargo test --frozen
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm644 "LICENSE-APACHE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE-APACHE"
  install -Dm644 "LICENSE-MIT" "$pkgdir/usr/share/licenses/$pkgname/LICENSE-MIT"
  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"

  install -Dm644 target/release/build/hyperfine-*/out/hyperfine.bash "$pkgdir/usr/share/bash-completion/completions/hyperfine"
  install -Dm644 target/release/build/hyperfine-*/out/hyperfine.fish "$pkgdir/usr/share/fish/vendor_completions.d/hyperfine.fish"
  install -Dm644 target/release/build/hyperfine-*/out/_hyperfine "$pkgdir/usr/share/zsh/site-functions/_hyperfine"

  install -Dm644 doc/hyperfine.1 "$pkgdir/usr/share/man/man1/hyperfine.1"

  install -Dm755 -t "$pkgdir/usr/lib/$pkgname/scripts" scripts/*.py
}
