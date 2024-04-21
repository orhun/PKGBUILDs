# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Gobidev <adrian[dot]groh[at]t-online[dot]de>
# Contributor: Hao Long <aur@esd.cc>

pkgname=rustscan
pkgver=2.2.2
pkgrel=1
pkgdesc='A modern port scanner'
arch=('x86_64')
url='https://github.com/rustscan/RustScan'
license=('GPL3')
depends=('gcc-libs' 'nmap')
makedepends=('git' 'cargo')
checkdepends=('python')
options=('!lto')
_commit=dcc558cb43b9d966bb3ce23fae534ed075ebec03
source=("$pkgname::git+$url#commit=$_commit")
b2sums=('d817dba3561d538b6b1d44803f7176e14d60b95999d9854ea96c763705760030444f9fa8f71516663ec0aac085a88a49a148a3aa29737e5bb36da34480e509e3')

pkgver() {
  cd "$pkgname"

  git describe --tags | sed 's/^v//'
}

prepare() {
  cd "$pkgname"

  # download dependencies
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
  install -vDm755 -t "$pkgdir/usr/bin" target/release/rustscan
}
