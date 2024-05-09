# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Andreas 'Segaja' Schleifer <archlinux at segaja dot de>

pkgname=aliyun-cli
_gitcommit=aba22ba463d6af2a2bf1a7d8d1a50a08969aaa7d
pkgver=3.0.205
pkgrel=1
pkgdesc='Alibaba Cloud CLI'
arch=('x86_64')
url='https://github.com/aliyun/aliyun-cli'
license=('Apache-2.0')
depends=('glibc')
makedepends=('git' 'go')
source=("git+${url}#commit=${_gitcommit}"
        git+https://github.com/aliyun/aliyun-openapi-meta)
sha512sums=('667c9d45920f67f2d093bbda71eb787e8369a4bf9e65c374ee6a72228bb8b9da3109c73542b10ecef4055badf71bfbca47e38576646372e31674a8d0a0ca090e'
            'SKIP')
b2sums=('999d885ef8736cb4382cc5ab3a21c4cfaf25b8ca83b4f27d1acd6212446cd841063b433511d8d782ea2f7ec4061023c5cec87e01746587ec7d8428c4cb42baf8'
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
