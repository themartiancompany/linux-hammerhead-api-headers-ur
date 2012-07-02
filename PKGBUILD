# Maintainer: Allan McRae <allan@archlinux.org>

# toolchain build order: linux-api-headers->glibc->binutils->gcc->binutils->glibc

pkgname=linux-api-headers
pkgver=3.4.4
_basever=3.4
pkgrel=1
pkgdesc="Kernel headers sanitized for use in userspace"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/libc"
license=('GPL2')
source=(http://www.kernel.org/pub/linux/kernel/v3.x/linux-${_basever}.tar.xz
        http://www.kernel.org/pub/linux/kernel/v3.x/patch-${pkgver}.xz)
        # NOTE: signatures are not automatically verified by makepkg
        #http://www.kernel.org/pub/linux/kernel/v3.x/linux-${_basever}.tar.sign
        #http://www.kernel.org/pub/linux/kernel/v3.x/patch-${pkgver}.sign
md5sums=('967f72983655e2479f951195953e8480'
         '58e6672d932d74d5e2b6811b9d37d67c')

build() {
  cd ${srcdir}/linux-${_basever}
  [[ $pkgver != $_basever ]] && patch -p1 -i ${srcdir}/patch-${pkgver}

  make mrproper
  make headers_check
}

package() {
  cd ${srcdir}/linux-${_basever}
  make INSTALL_HDR_PATH=${pkgdir}/usr headers_install

  # use headers from libdrm
  rm -rf ${pkgdir}/usr/include/drm
  
  # clean-up unnecessary files generated during install
  find ${pkgdir} \( -name .install -o -name ..install.cmd \) -delete
}
