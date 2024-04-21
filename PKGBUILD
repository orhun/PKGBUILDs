# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Carl Smedstad <carl.smedstad at protonmail dot com>
# Contributor:  Po-An,Yang(Antonio) <yanganto gmail.com>

pkgname=clipcat
pkgver=0.17.0
pkgrel=1
pkgdesc="A clipboard manager"
arch=('x86_64')
url="https://github.com/xrelkd/clipcat"
license=('GPL-3.0-only')
depends=('gcc-libs')
makedepends=('cargo' 'libgit2' 'protobuf')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('9ad4aed9214d4c82340bd7c959f478055364c663537ed1ca159dd1175c8b0e38')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --frozen --release --all-features
  for cmd in clipcatd clipcatctl clipcat-menu clipcat-notify; do
    "target/release/$cmd" completions bash > "$cmd.bash"
    "target/release/$cmd" completions zsh > "$cmd.zsh"
    "target/release/$cmd" completions fish > "$cmd.fish"
  done
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen --all-features -- \
    --skip test_x11_clipboard \
    --skip test_x11_primary
}

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 -t "$pkgdir/usr/bin" \
    target/release/clipcat-menu \
    target/release/clipcat-notify \
    target/release/clipcatctl \
    target/release/clipcatd

  for cmd in clipcatd clipcatctl clipcat-menu clipcat-notify; do
    install -Dm644 "$cmd.bash" "$pkgdir/usr/share/bash-completion/completions/$cmd"
    install -Dm644 "$cmd.zsh" "$pkgdir/usr/share/zsh/site-functions/_$cmd"
    install -Dm644 "$cmd.fish" "$pkgdir/usr/share/fish/completions/$cmd.fish"
  done

  install -Dm644 -t "$pkgdir/usr/share/doc/$pkgname" ./*.md
}

# vim:set ts=2 sw=2 et:
