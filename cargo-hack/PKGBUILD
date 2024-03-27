# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Constantine Fedotov <zenflak@gmail.com>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-hack
pkgver=0.6.23
_commit=8c684c46b7fa206ed03d3f37317d269ddeb13adf
pkgrel=1
pkgdesc="A cargo subcommand to provide various options useful for testing and CI"
arch=('x86_64')
url="https://github.com/taiki-e/cargo-hack"
license=('MIT' 'Apache-2.0')
depends=('gcc-libs')
makedepends=('cargo' 'git')
source=("$pkgname::git+$url.git#commit=$_commit"
        "Cargo.lock")
sha512sums=('3e2d2f69fd9e608d47bfdafdf9f6bfa68a2cd30de8fd6e6d7056144e3bfa5fdaab2941814ad297bc354551f4935f0fceb17413e758c5454dbb4148355ac255c1'
            '86ebd9f0458694e3091bdfabfc27a87086086c04fce83b8ce119f2b6abb9dab31e2e91a5aca88217f6898f59e4e1793c4a4df138230a67319da4d55cdaaeb2dd')

prepare() {
  cd "$pkgname"
  cp "$srcdir/Cargo.lock" .
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "$pkgname"
  cargo build --release --frozen
}

check() {
  cd "$pkgname"
  cargo test --frozen -- \
    --skip "multi_target" \
    --skip "version_range" \
    --skip "version_range_failure"
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE-MIT -t "$pkgdir/usr/share/licenses/$pkgname"
  depends+=(rustup)
}

# vim: ts=2 sw=2 et:
