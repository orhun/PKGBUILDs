# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andreas 'Segaja' Schleifer <archlinux at segaja dot de>

pkgname=aliyun-cli
_gitcommit=635d1d3df297be8215e4c1b33ba5ce9f7430c6df
pkgver=3.0.214
pkgrel=1
pkgdesc='Alibaba Cloud CLI'
arch=('x86_64')
url='https://github.com/aliyun/aliyun-cli'
license=('Apache-2.0')
depends=('glibc')
makedepends=('git' 'go')
source=("git+${url}#commit=${_gitcommit}"
        git+https://github.com/aliyun/aliyun-openapi-meta)
sha512sums=('3c64eb69252396f8f068e369a76c8863b4e2e7c603a9132d79a0c9bc0c947d67e947ecb419e0649fbf18c5ae67f8ea63234794964e4c98a95df51efccb11175f'
            'SKIP')
b2sums=('ead0894107a4ff141a6877837b89a5a4c84119d8ef4dfd26081e6a1018ce884f121e1c9e0727cc758943a809fafca59c4422e93af3265c5396a45d5d82bd0919'
        'SKIP')

pkgver() {
  cd ${pkgname}
  git describe --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd ${pkgname}
  git submodule init
  git config submodule."aliyun-openapi-meta".url "${srcdir}/aliyun-openapi-meta"
  git -c protocol.file.allow=always submodule update --init --recursive
}

build() {
  cd ${pkgname}
  export CGO_LDFLAGS="${LDFLAGS}"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -mod=readonly -modcacherw -ldflags=-linkmode=external"

  go build \
    -ldflags "-linkmode=external -extldflags '${LDFLAGS}' -X 'github.com/aliyun/aliyun-cli/cli.Version=${pkgver}'" \
    -o ./out/aliyun ./main/main.go
}

# https://github.com/aliyun/aliyun-cli/issues/736
# check() {
#   cd ${pkgname}
#
#   # Horrible but needed for the ./cli/ tests
#   touch "${HOME}/.bashrc"
#
#   # for now can't test the `./oss/...` folder, because it needs an env file that is not so easy to have in dev
#   go test \
#     ./cli/... ./config/... ./i18n/... ./main/... ./openapi/... ./resource/...
# }

package() {
  cd ${pkgname}
  install -Dm 755 out/aliyun "${pkgdir}/usr/bin/aliyun"
  install -Dm 644 README*.md CHANGELOG.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 bin/README.md -t "${pkgdir}/usr/share/doc/${pkgname}/bin"
}

# vim: ts=2 sw=2 et:
