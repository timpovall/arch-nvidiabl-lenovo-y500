# Maintainer: Padfoot <padfoot at exemail dot com dot au>
# Contributor: Mr_Men <tetcheve at gmail dot com>
# Contributor: Hasan Gormus aka hsngrms <hsngrms at yandex dot com>
# Contributor: uwinkelvos <uwinkelvos at gmx dot de>

pkgname=nvidiabl
pkgver=0.88
pkgrel=3
pkgdesc="Backlight driver for NVidia graphics adapters"

arch=('x86_64' 
      'i686')
url="https://github.com/guillaumezin/nvidiabl"
license=('GPL')

makedepends=('linux-headers'
             'unzip')
conflicts=('nvidia-bl' 'nvidiablctl')

install=nvidiabl.install
source=(https://github.com/guillaumezin/nvidiabl/archive/master.zip 
        nvidiabl-master.patch)
md5sums=('5fdda33fedcb78320c1581e84b395d39'
         '79e5699da970908d6ec8dba114df87cb')

prepare() {
  cd "${srcdir}/nvidiabl-master/"
  patch -p1 -i "${srcdir}/nvidiabl-master.patch"
  echo "Adding settings specific to: Lenovo Y500 with geforce 650M..."
  echo 'NVIDIABL_DECLARE_LAPTOP_MODEL("LENOVO", "20193", PCI_ANY_ID, NVIDIABL_SC_AUTO, NVIDIABL_AUTO, NVIDIABL_AUTO, 0x1FFFF),' >> nvidiabl-laptops.h
  echo 'NVIDIABL_DECLARE_GPU_MODEL(0x0fd1, nv5x_driver_data),' >> nvidiabl-gpu.h
  echo "Done"
}

build() {
  cd "${srcdir}/nvidiabl-master/"
  make
}

package() {
  cd "${srcdir}/nvidiabl-master/"
  _extramodules="extramodules-$(uname -r | cut -f-2 -d'.')-$(uname -r|sed -e 's/.*-//g')"
  _MODPATH="${pkgdir}/usr/lib/modules/${_extramodules}/"
  install -d "${_MODPATH}"
  install -d "${pkgdir}/usr/bin/"

  install -m 644 "${srcdir}/nvidiabl-master/nvidiabl.ko" "${_MODPATH}"
  install -m 755 scripts/usr/local/sbin/nvidiablctl "${pkgdir}/usr/bin/"
}
