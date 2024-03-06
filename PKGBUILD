# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: MithicSpirit <rpc01234 at gmail dot com>
# Contributor: David Runge <dvzrv@archlinux.org>
# Contributor: Leonidas Spyropoulos <artafinde@archlinux.org>
# Contributor: Daniel M. Capella <polyzen@archlinux.org>

pkgbase=uv
pkgname=("$pkgbase" "python-$pkgbase")
pkgver=0.1.15
_commit=a8ac7b1eb421d60b46d04805b86ea15bbfd8d1e1
pkgrel=1
pkgdesc='An extremely fast Python package installer and resolver written in Rust'
arch=('x86_64')
url="https://github.com/astral-sh/uv"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs' # 'libgcc_s.so'
         'glibc' # 'libc.so' 'libm.so'
         'zlib' 'libz.so')
makedepends=('cargo' 'maturin' 'python-installer' 'cmake' 'git')
checkdepends=('python' 'python-zstandard' 'libxcrypt-compat' 'clang')
options=('!lto')
source=("$pkgname::git+$url.git#commit=$_commit")
sha512sums=('SKIP')

prepare() {
  cd "$pkgbase"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgbase"
  maturin build --locked --release --all-features --target "$(rustc -vV | sed -n 's/host: //p')" --strip
}

check() {
  cd "$pkgbase"
  python3 ./scripts/bootstrap/install.py
  cargo test -p uv --frozen --all-features
}

_package_common() {
  install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE-*
  install -Dm0644 -t "$pkgdir/usr/share/doc/$pkgname/" README.md
}

package_uv() {
  cd "$pkgbase"
  _package_common
  local _target="target/$(rustc -vV | sed -n 's/host: //p')/release/uv"
  install -Dm0755 -t "$pkgdir/usr/bin/" "$_target"
}

package_python-uv() {
  cd "$pkgbase"
  _package_common
  depends=(python "$pkgbase")
  python -m installer -d "$pkgdir" target/wheels/*.whl
  rm -rf "$pkgdir/usr/bin"
}

# vim: ts=2 sw=2 et:
