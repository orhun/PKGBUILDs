# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: MithicSpirit <rpc01234 at gmail dot com>
# Contributor: David Runge <dvzrv@archlinux.org>
# Contributor: Leonidas Spyropoulos <artafinde@archlinux.org>
# Contributor: Daniel M. Capella <polyzen@archlinux.org>

pkgbase=uv
pkgname=("$pkgbase" "python-$pkgbase")
pkgver=0.1.27
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
source=("git+$url.git#tag=$pkgver")
sha256sums=('1caf4377edc747dd7f2c840c4a7d72f766ad86f3c860d8a5ae406f1a120c2b6e')

prepare() {
  cd "$pkgbase"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
  mkdir completions
}

build() {
  cd "$pkgbase"
  maturin build --locked --release --all-features --target "$(rustc -vV | sed -n 's/host: //p')" --strip
  local compgen="target/$(rustc -vV | sed -n 's/host: //p')/release/uv --generate-shell-completion"
  $compgen bash >"completions/$pkgbase"
  $compgen elvish >"completions/$pkgbase.elv"
  $compgen fish >"completions/$pkgbase.fish"
  $compgen zsh >"completions/_$pkgbase"
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
  install -Dm 644 "completions/$pkgbase" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -Dm 644 "completions/$pkgbase.elv" -t "$pkgdir/usr/share/elvish/lib/"
  install -Dm 644 "completions/$pkgbase.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d/"
  install -Dm 644 "completions/_$pkgbase" -t "$pkgdir/usr/share/zsh/site-functions/"
}

package_python-uv() {
  cd "$pkgbase"
  _package_common
  depends=(python "$pkgbase")
  python -m installer -d "$pkgdir" target/wheels/*.whl
  rm -rf "$pkgdir/usr/bin"
}

# vim: ts=2 sw=2 et:
