# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Daniele Basso <d dot bass05 at proton dot me>
# Contributor: T. Jameson Little <t.jameson.little at gmail dot com>
# Contributor: Usagi Ito <usagi@WonderRabbitProject.net>
# Contributor: siasia <http://pastebin.com/qsBEmNCw>
# Contributor: Julien Nicoulaud <julien.nicoulaud@gmail.com>

pkgname=dart
pkgver=3.0.7
_commit=53cf56f86114e95bfcdf974948be3a7755ca91e2
pkgrel=1
pkgdesc='The dart programming language SDK'
arch=('x86_64')
url='https://www.dartlang.org/'
depends=('glibc')
license=('BSD')
makedepends=(
  'clang'
  'dart'
  'git'
  'gn'
  'lld'
  'llvm'
  'ninja'
  'python'
  'python-httplib2'
  'python-six'
)
source=(
  "$pkgname::git+https://github.com/dart-lang/sdk.git"
  "git+https://chromium.googlesource.com/chromium/tools/depot_tools.git"
)
sha512sums=('SKIP'
            'SKIP')

prepare() {
cat >.gclient <<EOF
solutions = [
  {
    "name": "sdk",
    "url": "file://${srcdir}/$pkgname@${_commit}",
    "deps_file": "DEPS",
    "managed": False,
    "custom_deps": {},
    "custom_vars": {},
  },
]
EOF

  export PATH+=":$PWD/depot_tools" DEPOT_TOOLS_UPDATE=0

  depot_tools/gclient.py sync -D \
      --nohooks \
      --with_branch_heads \
      --with_tags

  dart sdk/tools/generate_package_config.dart
  python sdk/tools/generate_sdk_version_file.py

  cd sdk
  # ------
  # Credits: Lauren N. Liberda <lauren@selfisekai.rocks> on Alpine Linux

  # shut up on clang
  chmod u+w buildtools/linux-x64/clang/.versions/clang.cipd_version
  echo '{"instance_id":"system"}' > buildtools/linux-x64/clang/.versions/clang.cipd_version
  chmod u-w buildtools/linux-x64/clang/.versions/clang.cipd_version

  # bind bootstrapped interpreter
  ln -sf /usr/bin/dart tools/sdks/dart-sdk/bin/dart
  ln -sf /usr/bin/dart2js tools/sdks/dart-sdk/bin/dart2js
  # ------

  sed -i 's|prefix = rebased_clang_dir|prefix= ""|g' build/toolchain/linux/BUILD.gn # use system clang
  sed -i 's|}/|}|g' build/toolchain/linux/BUILD.gn # use system clang
  sed -i 's|rebase|#|g' build/toolchain/linux/BUILD.gn

}

build() {
  cd sdk

  gn gen -qv out --args='target_os = "linux"
                        host_cpu = "x64"
                        target_cpu = "x64"
                        dart_target_arch = "x64"
                        dart_use_compressed_pointers = true
                        dart_use_crashpad = false
                        dart_snapshot_kind = "app-jit"
                        dart_debug_optimization_level= "2"
                        dart_use_fallback_root_certificates = true
                        dart_use_compressed_pointers = true
                        dart_use_tcmalloc = true
                        dart_use_mallinfo2 = true
                        is_debug = false
                        is_release = false
                        is_product = true
                        dart_debug = false
                        dart_runtime_mode = "release"
                        exclude_kernel_service = false
                        is_clang = true
                        dart_vm_code_coverage = false
                        is_asan = false
                        is_lsan = false
                        is_msan = false
                        is_tsan = false
                        is_ubsan = false
                        is_qemu = false
                        dart_platform_sdk = false
                        dart_use_debian_sysroot = false
                        verify_sdk_hash = false'

  sed -i 's|ldflags}|ldflags} -fuse-ld=lld|g' out/toolchain.ninja # use system ldd
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
