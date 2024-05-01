# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andreas 'Segaja' Schleifer <archlinux at segaja dot de>

pkgname=aliyun-cli
_gitcommit=57470075406dc10f1c95486c218521d8f43d12c7
pkgver=3.0.204
pkgrel=1
pkgdesc='Alibaba Cloud CLI'
arch=('x86_64')
url='https://github.com/aliyun/aliyun-cli'
license=('Apache-2.0')
depends=('glibc')
makedepends=('git' 'go')
source=("git+${url}#commit=${_gitcommit}"
        git+https://github.com/aliyun/aliyun-openapi-meta)
sha512sums=('ebca68ef5443bcc47699c5ea09e5ab2777275a12207afe9e281776e5f94872f1a6349e943a65616e933ab114098e4fe21ca267e8b19e2364465d2ab2d1d91c90'
            'SKIP')
b2sums=('2372412bb4b7c313a41936e92f9a7e17d5a11479be3630f3d2ca1059aa9d273c364b4d7d0b5aac59b9dcc67e69c58472dec7bba6597ed50c0d7a764bfaf57622'
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
