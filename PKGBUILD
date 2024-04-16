# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Daniele Basso <d dot bass05 at proton dot me>
# Contributor: T. Jameson Little <t.jameson.little at gmail dot com>
# Contributor: Usagi Ito <usagi@WonderRabbitProject.net>
# Contributor: siasia <http://pastebin.com/qsBEmNCw>
# Contributor: Julien Nicoulaud <julien.nicoulaud@gmail.com>

pkgname=dart
pkgver=3.3.3
_commit=c09cb46304325cc59890ef685d33f5e022da047e # https://github.com/dart-lang/sdk/commits/stable/
pkgrel=1
pkgdesc='The dart programming language SDK'
arch=('x86_64')
url='https://dart.dev/'
depends=('glibc')
license=('BSD')
makedepends=(
  'dart'
  'git'
  'gn'
  'ninja'
  'python'
  'python-httplib2'
  'python-six'
)
source=(
  "git+https://github.com/dart-lang/sdk.git#commit=$_commit"
  "git+https://chromium.googlesource.com/chromium/tools/depot_tools.git"
  "DEPS.patch"
)
sha256sums=('aaba03bb91dd3fbabaf880e21a7a40f605a71fdeb4ab66629090be3f7123ee84'
            'SKIP'
            'db6576a70c6719e26795b9824546058b79fefa64158c1002d36546d826084403')

prepare() {
cat >.gclient <<EOF
solutions = [
  {
    "name": "sdk",
    "url": "file://${srcdir}/sdk",
    "deps_file": "DEPS",
    "managed": False,
    "custom_deps": {},
    "custom_vars": {},
  },
]
EOF

  export PATH+=":$PWD/depot_tools" DEPOT_TOOLS_UPDATE=0

  cd sdk

  patch -Np 1 --input=$srcdir/DEPS.patch

  python ../depot_tools/gclient.py sync -D \
      --nohooks \
      --no-history \
      --shallow \
      -r ${srcdir}/sdk@${_commit}

  dart tools/generate_package_config.dart
  python tools/generate_sdk_version_file.py

  sed -i 's|prefix = rebased_clang_dir|prefix= ""|g' build/toolchain/linux/BUILD.gn # use system clang
  sed -i 's|}/|}|g' build/toolchain/linux/BUILD.gn # use system clang
  sed -i 's|rebase|#|g' build/toolchain/linux/BUILD.gn
}

build() {
  cd sdk

  # gn args --list out

  /usr/bin/gn gen -qv out --args='
                        target_cpu = "x64"
                        is_debug = false
                        is_release = true
                        is_clang = false
                        dart_platform_sdk = false
                        verify_sdk_hash = false'
  ninja create_sdk -v -C out
}

package() {
  # cd to directory
  cd sdk/out/

  # Create directories
  install -d "$pkgdir"{"/opt/$pkgname-sdk",/usr/{bin,"share/doc/$pkgname"}}

  # Package the files
  cp -a "$pkgname-sdk/"* "$pkgdir/opt/$pkgname-sdk/"

  # Set up symbolic links for the executables
  for f in dart dartaotruntime; do
    ln -s "/opt/$pkgname-sdk/bin/$f" "$pkgdir/usr/bin/$f"
  done

  # Package documentation
  install -Dm644 "$pkgdir/opt/$pkgname-sdk/README" -t "$pkgdir/usr/share/doc/$pkgname"

  # BSD License
  install -Dm644 ../LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
