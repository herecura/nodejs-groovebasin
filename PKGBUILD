# vim:set ts=2 sw=2 et:
# Maintainer: Jeremy "Ichimonji10" Audet <ichimonji10 at gmail dot com>
# Contributor: Andrew Kelley <superjoe30@gmail.com>
# Contributor: superjoe <superjoe30@gmail.com>
#
# makepkg warns "Package contains reference to $pkgdir". This is OK. See:
# https://github.com/andrewrk/groovebasin/issues/214

pkgname=nodejs-groovebasin
_pkgname="${pkgname#nodejs-}"
pkgver=1.3.1
pkgrel=1
pkgdesc='Music player server with a web-based user interface inspired by Amarok 1.4'
arch=('i686' 'x86_64')
url='http://groovebasin.com/'
license=(MIT)
depends=('nodejs' 'libgroove')
makedepends=('python2')
source=("https://github.com/andrewrk/groovebasin/archive/${pkgver}.tar.gz"
        groovebasin)

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  export PYTHON=python2
  npm run build
}

package() {
  # install application
  local _npmdir="${pkgdir}/usr/lib/node_modules/"
  mkdir -p "${srcdir}/${_npmdir}"
  cd "${srcdir}/${_npmdir}"
  npm install --user root --global --prefix "${pkgdir}/usr" "${_pkgname}@${pkgver}"

  # install executable
  install -Dm755 "${srcdir}/groovebasin" "${pkgdir}/usr/bin/${_pkgname}"

  # install license
  install -Dm 644 "${srcdir}/${_pkgname}-${pkgver}/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

sha256sums=('d5eb37f52e2b590722e5a8cdf33043aa300e051d667a2c947001e1de1d1ff544'
            'b121429dc1c6ed132a02f66c8b49424c46bf9a1e358d9fe91cf4b8093eaa4e28')
