# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Wesley Moore <wes@wezm.net>

pkgname=git-grab
pkgver=2.0.0
pkgrel=1
pkgdesc='A tool to clone git repositories to a standard location organised by domain and path'
arch=('x86_64')
url='https://github.com/wezm/git-grab'
license=('MIT' 'Apache')
depends=('git' 'gcc-libs')
makedepends=('cargo')
options=('!lto')
_commit=f6f6fa1473b4504710f68223d3f92c2355194912
source=("$pkgname::git+$url.git#commit=$_commit")
b2sums=('SKIP')

pkgver() {
  cd "$pkgname"

  git describe --tags | sed 's/^v//'
}

prepare() {
  cd "$pkgname"

  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname"

  cargo build --frozen --release --all-features
}

check() {
  cd "$pkgname"

  cargo test --frozen --all-features
}

package() {
  cd "$pkgname"

  # binary
  install -vDm755 -t "$pkgdir/usr/bin" target/release/git-grab

  # documentation
  install -vDm644 -t "$pkgdir/usr/share/doc/$pkgname" README.md

  # license
  install -vDm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE*
  sed -n '/^Licence/,/^at your option./p' \
    README.md \
    > "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
