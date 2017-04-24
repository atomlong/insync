# Maintainer: Nate Levesque <public@thenaterhood.com>
# Contributor: Vlad M. <vlad@archlinux.net>
# Contributor: Zhengyu Xu <xzy3186@gmail.com>

pkgname=insync
pkgver=1.3.15
_pkgver=36150
pkgrel=1
pkgdesc="An unofficial Google Drive client that runs on Linux, with support for various desktops"
url="https://www.insynchq.com/downloads"
license=('custom:insync')
options=(!strip !upx)
depends=('xdg-utils' 'glibc' 'python2')
arch=('i686' 'x86_64')
source=('insync@.service' 'insync.service')
source_i686=("http://s.insynchq.com/builds/${pkgname}_${pkgver}.${_pkgver}-trusty_i386.deb")
source_x86_64=("http://s.insynchq.com/builds/${pkgname}_${pkgver}.${_pkgver}-trusty_amd64.deb")
sha256sums=('cf276c1dbf1592ea63a21c2d61c75f7ad6ec3b13e87b3aaa331e9c14799f4598'
            '1432141539a6b3c5333631a2ee6696fab9bd2fe8770643bc670d95e4e96203e0')
sha256sums_i686=('a1c237e2acd0eb6b1bd53aa1ef8943bdb9049e199d7e1b650e0673fe384532ed')
sha256sums_x86_64=('e961c6a7fb354bb7a3bab090a87f6179207160c2ffbb08674b99329b1c4b2f74')

package() {
   tar xvf data.tar.gz
   cp -rp usr $pkgdir

   # Patch files for Arch
   cd $pkgdir
   echo "==> Patching files..."
   for file in $(grep -R "/usr/bin/python" . | cut -f1 -d :)
   do
      grepPrefix=$(echo $file | cut -f1 -d" ")
      [ -z $grepPrefix ] && sed -i "s|usr/bin/python$|usr/bin/python2|g" $file
   done
   # End of patching

   mkdir -p ${pkgdir}/usr/lib/systemd/system
   mkdir -p ${pkgdir}/usr/lib/systemd/user
   cp ${srcdir}/insync@.service ${pkgdir}/usr/lib/systemd/system/insync@.service
   cp ${srcdir}/insync.service ${pkgdir}/usr/lib/systemd/user/insync.service
   ln -sf "/usr/lib/libfontconfig.so.1" "${pkgdir}/usr/lib/insync/libfontconfig.so.1"
}
