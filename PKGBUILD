# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Jonathon Fernyhough <jonathon_at_manjaro_dot_org>
# Contributor: Jon Gjengset <jon@tsp.io>
pkgname=rustup
pkgver=1.27.0
pkgrel=1
pkgdesc="The Rust toolchain installer"
arch=('x86_64')
url="https://github.com/rust-lang/rustup.rs"
license=('MIT' 'Apache-2.0')
depends=('curl' 'xz' 'zstd')
makedepends=('cargo')
optdepends=('lldb: rust-lldb script'
            'gdb: rust-gdb script')
provides=('rust' 'cargo' 'rust-nightly' 'cargo-nightly' 'rustfmt' 'rust-src'
          'lib32-rust-libs' 'rust-musl' 'rust-wasm' 'rust-analyzer')
conflicts=('rust' 'cargo' 'rustfmt')
replaces=('cargo-tree')
install='post.install'
options=("!lto")
source=("rustup-${pkgver}.tar.gz::https://github.com/rust-lang/rustup.rs/archive/${pkgver}.tar.gz"
        "rustup-profile.sh")
sha512sums=('0b9349364e0f9d60ba0d486064295413012d38ec97597207b3c82e07ebcf6b5ade403a46fb3910fe4d63607150ce5b0e367ac322f894599bd6b02dae3872e8f0'
            '18d5b4ab9a032cb43fd0b59fb553a878068981534e549935c5ff4a12dc2f74849ce36367eb59e670d674a19a7d4bc0056d0694d7f87ede187416c2ffcbb20355')
_binlinks=('cargo' 'rustc' 'rustdoc' 'rust-gdb' 'rust-lldb' 'rustfmt' 'cargo-fmt' 'cargo-clippy' 'clippy-driver' 'cargo-miri')

build() {
  cd "$pkgname-${pkgver}"
  cargo build --release --features no-self-update --bin rustup-init
}

package() {
  cd "$pkgname-${pkgver}"
  install -d "${pkgdir}/usr/lib/$pkgname/bin"
  install -Dm755 "target/release/rustup-init" "${pkgdir}/usr/bin/rustup"
  for link in "${_binlinks[@]}"; do
      ln -s /usr/bin/rustup "${pkgdir}/usr/bin/${link}"
  done

  # Special treatment for rust-analyzer to still allow the separate package version to be used.
  ln -s /usr/bin/rustup "${pkgdir}/usr/lib/$pkgname/bin/rust-analyzer"

  install -Dm644 "$srcdir/$pkgname-profile.sh" "$pkgdir/etc/profile.d/$pkgname.sh"

  # Generate completion files.
  mkdir -p "$pkgdir/usr/share/bash-completion/completions"
  "$pkgdir"/usr/bin/rustup completions bash > "$pkgdir/usr/share/bash-completion/completions/rustup"
  "$pkgdir"/usr/bin/rustup completions bash cargo > "$pkgdir/usr/share/bash-completion/completions/cargo"
  mkdir -p "$pkgdir/usr/share/fish/vendor_completions.d"
  "$pkgdir"/usr/bin/rustup completions fish > "$pkgdir/usr/share/fish/vendor_completions.d/rustup.fish"
  mkdir -p "$pkgdir/usr/share/zsh/site-functions"
  "$pkgdir"/usr/bin/rustup completions zsh > "$pkgdir/usr/share/zsh/site-functions/_rustup"
  "$pkgdir"/usr/bin/rustup completions zsh cargo > "$pkgdir/usr/share/zsh/site-functions/_cargo"

  install -Dm644 LICENSE-MIT "${pkgdir}"/usr/share/licenses/$pkgname/LICENSE-MIT
  install -Dm644 LICENSE-APACHE "${pkgdir}"/usr/share/licenses/$pkgname/LICENSE-APACHE
}

# vim:set ts=2 sw=2 et:
