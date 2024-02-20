# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: MithicSpirit <rpc01234 at gmail dot com>
# Contributor: David Runge <dvzrv@archlinux.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Leonidas Spyropoulos <artafinde@archlinux.org>
# Contributor: Daniel M. Capella <polyzen@archlinux.org>

pkgbase=uv
pkgname=("$pkgbase" "python-$pkgbase")
pkgver=0.1.6
pkgrel=1
pkgdesc='An extremely fast Python package installer and resolver written in Rust'
arch=('x86_64')
url="https://github.com/astral-sh/uv"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' 'glibc')
makedepends=('cargo' 'maturin' 'python-installer' 'cmake')
checkdepends=('python' 'python-zstandard' 'libxcrypt-compat' 'clang')
options=('!lto')
source=("$pkgbase-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver/$pkgbase-$pkgver.tar.gz")
sha512sums=('5c765176cf19ef917c1e938650082ed5b867be6d8a809b05fc179435bfbbb68480ac5d2d8b8973bdc7e38cc61f7b4d57dee7358638e67a55f178c8f9e0a8a6bb')
b2sums=('bdc8b7f09534464a5927ce7dacba7d4c6643379165dc356b30151b294c53f1b537ff6173287019051d1936164f47701061e8b27e60a421a479a1ab42c39819ab')

prepare() {
  cd "$pkgbase-$pkgver"
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
