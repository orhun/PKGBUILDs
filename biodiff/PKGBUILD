# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: willemw <willemw12@gmail.com>
# Contributor: Daniel Maslowski <info@orangecms.org>

pkgname=biodiff
pkgver=1.2.1
pkgrel=1
_commit=48468e9e7493c5bec608035f86459feb2469be14
pkgdesc='Hex diff viewer using alignment algorithms from biology'
arch=('x86_64')
url=https://github.com/8051Enthusiast/biodiff
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo' 'cmake' 'git')
source=(
  "$pkgname-$pkgver::git+$url#commit=$_commit"
  "${pkgname}-WFA2-lib::git+https://github.com/smarco/WFA2-lib"
)
sha256sums=('ba5f3f50e3f3acd487459de405988b9403fc815c3938cf0409e716f309a44493'
            'SKIP')
options=('!lto')
prepare() {
  cd "$pkgname-$pkgver"
  git submodule init
  git config submodule."biodiff-wfa2-sys/WFA2-lib".url "${srcdir}/${pkgname}"-WFA2-lib
  git -c protocol.file.allow=always submodule update --init --recursive
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim: ts=2 sw=2 et:
