# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Uffe Jakobsen <uffe at uffe dot org>
# Contributor: speps <speps at aur dot archlinux dot org>

pkgname=lnav
pkgver=0.12.2
pkgrel=1
pkgdesc="A curses-based tool for viewing and analyzing log files"
arch=('x86_64')
url="http://lnav.org/"
license=('custom:BSD')
depends=('ncurses' 'curl' 'pcre2' 'sqlite3' 'libarchive')
makedepends=('openssh')
source=("$pkgname-$pkgver.tar.gz::https://github.com/tstack/lnav/archive/v$pkgver.tar.gz")
sha256sums=('9f12e17f9f2b2f1ddf00ef3f35f61ab3c9709ddf2beaa0eeaf441462e812ca7f')

build() {
  cd $pkgname-$pkgver
  ./autogen.sh
  ./configure --prefix=/usr --disable-static
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir/" install
  install -Dm 644 README -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "$pkgname.1" -t "$pkgdir/usr/share/man/man1"
}

# vim:set ts=2 sw=2 et:
