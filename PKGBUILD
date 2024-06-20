# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andreas 'Segaja' Schleifer <archlinux at segaja dot de>

pkgname=aliyun-cli
_gitcommit=c3de4e38a8236df009087ae3a30702a116e1b960
pkgver=3.0.208
pkgrel=1
pkgdesc='Alibaba Cloud CLI'
arch=('x86_64')
url='https://github.com/aliyun/aliyun-cli'
license=('Apache-2.0')
depends=('glibc')
makedepends=('git' 'go')
source=("git+${url}#commit=${_gitcommit}"
        git+https://github.com/aliyun/aliyun-openapi-meta)
sha512sums=('aab3d570566caa573cb0a80523d0707083b0e41ef7467f195693d46ca546880ce8efa60c882d01f4dba415ea27bc1fa1e8572619e17d7c5e6786b0241a6edd97'
            'SKIP')
b2sums=('e2a2b2380526fc552edbc9ce767c5ea3d4882aceaf7543e5310a202aef252ac944206b5ecebaad7464233391ba5c8baed6c968a69eb0bbc37bed80b48c124e40'
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
