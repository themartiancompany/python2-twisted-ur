# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  LaughingMan
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer:  Pellegrino Prevete <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>

_py="python2"
_pkg="twisted"
pkgname="${_py}-${_pkg}"
# Do not update.
# This is the last twisted version
# supporting Python2.
pkgver=20.3.0
pkgrel=5
_pkgdesc=(
  "Asynchronous networking framework written"
  "in Python (20.3.0 is the last version"
  "supporting Python 2)"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7h'
  'armv6l'
  'powerpc'
  'mips'
  'i686'
)
url="https://${_pkg}matrix.com/"
license=('MIT')
depends=(
  'python-twisted'
  'python2-zope-interface'
  'python2-service-identity'
  'python2-incremental'
  'python2-constantly'
  'python2-automat'
  'python2-hyperlink'
  'python2-attrs'
  'python2-pyhamcrest'
)
makedepends=(
  'python2-setuptools'
)
optdepends=(
  "${_py}-pyopenssl: for TLS client hostname verification"
  "${_py}-idna: for TLS client hostname verification"
  "${_py}-cryptography: for using conch"
  "${_py}-pyasn1: for using conch"
  "${_py}-appdirs: for using conch"
  "${_py}-bcrypt: for using conch"
  "${_py}-priority: for http2 support"
  "${_py}-pyserial: for serial support"
  "${_py}-soappy: for twisted.web.soap"
  'tk: for using tkconch'
)
_http="https://github.com"
_ns="${_pkg}"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${pkgname}-${pkgver}.tar.gz::${_url}/archive/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  '72307a0b9165d5f6b31f5563f4f76f9c759349d55f6dcaf43358eab3e8f1b2065e0b12c8ac43f14061ee17cb2d9b27f463bcb9e642750fb8e6e510e403bd2b06'
)

prepare() {
  sed \
    -i \
      "s:^#!.*bin.*python:#!/usr/bin/${_py}:" \
    "${_pkg}-${_pkg}-${pkgver}/src/twisted/mail/test/pop3testserver.py" \
    "${_pkg}-${_pkg}-${pkgver}/src/twisted/trial/test/scripttest.py"
}

build() {
  cd \
    "${srcdir}/${_pkg}-${_pkg}-${pkgver}"
  python2 setup.py build
}

package() {
  local \
    _name \
    _twisted_bins=()
  _twisted_bins=(
    trial
    twistd
    twist \
    ckeygen
    cftp
    conch
    pyhtmlizer
    tkconch
    mailmail
  )
  cd \
    "${srcdir}/${_pkg}-${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
        --optimize=1

  # python-twisted already provides
  # these command line tools.
  # Let's depend on python-twisted and
  # rename the tools here so we don't conflict.
  for _name \
    in "${_twisted_bins[@]}"; do
    mv \
      "${pkgdir}/usr/bin/${_name}"{,2}
  done

  install \
    -D \
    -m644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set sw=2 sts=-1 et:
