# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=taskwarrior-tui
pkgver=0.25.1
pkgrel=1
pkgdesc="A terminal user interface for taskwarrior"
arch=('x86_64')
url="https://github.com/kdheepak/taskwarrior-tui"
license=('MIT')
depends=('task')
makedepends=('cargo' 'git')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz"
        "git+https://github.com/kdheepak/taskwarrior-testdata")
sha256sums=('52be07ec3331b830b1fa626e0da9a2196aa861db0bd04653445d009c74322361'
            'SKIP')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen --all-features
}

check() {
  cd "$pkgname-$pkgver"
  export TASKRC="../taskwarrior-testdata/.taskrc"
  export TASKDATA="../taskwarrior-testdata/.task"
  cargo test --frozen --all-features
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "docs/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
  install -Dm 644 "completions/$pkgname.bash" "${pkgdir}/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "${pkgdir}/usr/share/zsh/site-functions"
}

# vim: ts=2 sw=2 et:
