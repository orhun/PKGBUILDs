# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Wesley Moore <wes@wezm.net>

pkgname=git-grab
pkgver=3.0.0
pkgrel=1
pkgdesc='A tool to clone git repositories to a standard location organised by domain and path'
arch=('x86_64')
url='https://github.com/wezm/git-grab'
license=('MIT' 'Apache-2.0')
depends=('git' 'gcc-libs')
makedepends=('cargo')
options=('!lto')
_commit=abb36d2a6af715aae5a1b85228d69f778aa108b6
source=("$pkgname::git+$url.git#commit=$_commit")
b2sums=('f26a09a795e932a62d21769f959db10cec087d4b1943927240dc686b9bfae1dd8cab30eef067a9cb6c37bf8ca4277357dd405766e184ce16a7ddfd41af40e4e9')

pkgver() {
  cd "$pkgname"

  git describe --tags | sed 's/^v//'
}

prepare() {
  cd "$pkgname"

  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
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
