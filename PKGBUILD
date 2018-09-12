# Maintainer: Kojiro ONO <ono.kojiro@gmail.com>
#

_realname=qemu
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=3.0.0
pkgrel=1
pkgdesc='QEMU is a generic and open source machine emulator and virtualizer.'
arch=('any')
url='https://www.qemu.org/'
license=('GPL3')
depends=('python2')
source=("https://download.qemu.org/${_realname}-${pkgver}.tar.xz")
sha256sums=('8d7af64fe8bd5ea5c3bdf17131a8b858491bcce1ee3839425a6d91fb821b5713')

prepare() {
  cd $srcdir/${_realname}-${pkgver}
}

_configure(){
  ./configure --prefix=${MINGW_PREFIX} \
    --build=${MINGW_CHOST} \
    --host=${MINGW_CHOST} \
    --bindir=${MINGW_PREFIX}/bin \
    --libexecdir=${MINGW_PREFIX}/libexec \
    --sysconfdir=${MINGW_PREFIX}/etc \
    --localstatedir=${MINGW_PREFIX}/var \
    --libdir=${MINGW_PREFIX}/lib \
    --datadir=${MINGW_PREFIX}/share/${_realname} \
    --docdir=${MINGW_PREFIX}/share/doc/${_realname} \
    --mandir=${MINGW_PREFIX}/share/man/${_realname} \
    --disable-capstone \
    --python=/usr/bin/python2
}

build() {
  cd $srcdir/${_realname}-${pkgver}
  _configure
  make
}

package() {
  cd ${srcdir}/${_realname}-${pkgver}
  make install DESTDIR="${pkgdir}"

  # Licenses
  install -Dm644 "${srcdir}/${_realname}-${pkgver}/README" "${pkgdir}${MINGW_PREFIX}/share/licenses/${_realname}/README"
  install -Dm644 "${srcdir}/${_realname}-${pkgver}/COPYING" "${pkgdir}${MINGW_PREFIX}/share/licenses/${_realname}/COPYING"
}
