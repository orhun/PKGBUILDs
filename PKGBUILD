# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andreas 'Segaja' Schleifer <archlinux at segaja dot de>

pkgname=aliyun-cli
_gitcommit=bcb078372ae7381955ececa3b59a09b2c9bd87d5
pkgver=3.0.207
pkgrel=1
pkgdesc='Alibaba Cloud CLI'
arch=('x86_64')
url='https://github.com/aliyun/aliyun-cli'
license=('Apache-2.0')
depends=('glibc')
makedepends=('git' 'go')
source=("git+${url}#commit=${_gitcommit}"
        git+https://github.com/aliyun/aliyun-openapi-meta)
sha512sums=('b1259edad738c266788127f1db65d97d28cb184def11e84d1527ca45ea72b27c9c64e4ede062d1a264979529fdb3b06040a447756b651c40dcb6d9b7ced1d8e4'
            'SKIP')
b2sums=('444d8822b5d7804232727d70e0c9450679546757efbfec0c06c9b9fac117129c91288f27a3574581ed4d7bee9ed5f4d5dd0fabbce0f203bad84264bf350b69ea'
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
