# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Gobidev <adrian[dot]groh[at]t-online[dot]de>
# Contributor: Hao Long <aur@esd.cc>

pkgname=rustscan
pkgver=2.2.3
pkgrel=2
pkgdesc='A modern port scanner'
arch=('x86_64')
url='https://github.com/rustscan/RustScan'
license=('GPL3')
depends=('gcc-libs')
makedepends=('git' 'cargo')
optdepends=('nmap: Script engine support')
checkdepends=('python')
options=('!lto')
_commit=5328bfc8b00c99163edf770e859960280d55360b
source=("$pkgname::git+$url#commit=$_commit")
b2sums=('960a175f59406d502d3b30dd2b9d13f5e152bdac1cd6e230e06c5b2291ffb254553e7c4163fcc40d9f3a65067823e041f7c95782e2f2299b50c401221a1738c5')

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
