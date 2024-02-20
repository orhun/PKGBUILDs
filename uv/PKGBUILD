# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: MithicSpirit <rpc01234 at gmail dot com>
# Contributor: David Runge <dvzrv@archlinux.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Leonidas Spyropoulos <artafinde@archlinux.org>
# Contributor: Daniel M. Capella <polyzen@archlinux.org>

pkgbase=uv
pkgname=("$pkgbase" "python-$pkgbase")
pkgver=0.1.5
pkgrel=3
pkgdesc='An extremely fast Python package installer and resolver written in Rust'
arch=('x86_64')
url="https://github.com/astral-sh/uv"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'glibc')
makedepends=('cargo' 'maturin' 'python-installer' 'cmake')
checkdepends=('python' 'python-zstandard' 'libxcrypt-compat' 'clang')
options=('!lto')
source=("$pkgbase-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver/$pkgbase-$pkgver.tar.gz"
        "$pkgbase-$pkgver-fix-tests.patch::https://github.com/astral-sh/uv/commit/b76efc62a72ed8031aa91ae80bb1b4a159bd3d21.patch")
sha512sums=('236aacb50faf140e014621e96f1ddff451c10f83f3662c9c8b40582b5959cec6e40410f4b1d84b6fe6fc10823e9b68da4278f16807359f9e52ec7bea1f425130'
            '9f4b1124c4a0a18392d87de8c8474b88675bbee0c909b2ea905dbf1f2389a5efdeb4df5bf61f9618a9ee2ab5d3cfb8177e09403789a66074276716950791bcb4')
b2sums=('e3d801b26c5dce5fdc2aab2d6be93f3a119f31185ba56a46d463c01fef76a04848a828e0cd2af6b6169684b565365902a293d42b0e46ce778d5282a114ad2c09'
        '1c3cd083db77c4acef5e3f01d438c1fa86d8eb12cb2563704a50f692429e8ea8c5fad097504da6ca24fea7f4287d4a8e44fd25aa92ce8f7c14648ddb78da1fef')

prepare() {
  cd "$pkgbase-$pkgver"
  patch -Np1 -i "$srcdir/$pkgbase-$pkgver-fix-tests.patch"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgbase-$pkgver"
  maturin build --locked --release --all-features --target "$(rustc -vV | sed -n 's/host: //p')" --strip
}

check() {
  cd "$pkgbase-$pkgver"
  python3 ./scripts/bootstrap/install.py
  cargo test -p uv --frozen --all-features
}

_package_common() {
  install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE-*
  install -Dm0644 -t "$pkgdir/usr/share/doc/$pkgname/" README.md
}

package_uv() {
  cd "$pkgbase-$pkgver"
  _package_common
  local _target="target/$(rustc -vV | sed -n 's/host: //p')/release/uv"
  install -Dm0755 -t "$pkgdir/usr/bin/" "$_target"
}

package_python-uv() {
  cd "$pkgbase-$pkgver"
  _package_common
  depends=(python "$pkgbase")
  python -m installer -d "$pkgdir" target/wheels/*.whl
  rm -rf "$pkgdir/usr/bin"
}

# vim: ts=2 sw=2 et:
