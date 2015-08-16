# Maintainer: Frank Shin <frankshin82(at)gmail(dot)com
# Contributor: Rhon <rhon(at)free(dot)fr
pkgname=libcrystalhd-git
pkgver=20130503
pkgrel=3
pkgdesc="Broadcom CrystalHD library"
arch=('i686' 'x86_64')
url="http://git.linuxtv.org/cgit.cgi/jarod/crystalhd.git"
license=('GPL2')
depends=('gcc-libs')
makedepends=('git' 'make')
source=('crystalhd-3cb6786-crosscompiling-0.1.patch' 'crystalhd-3cb6786-fix_typo.patch' 'crystalhd-3cb6786-lower_THRESHOLD_globals.patch' 'crystalhd-3cb6786-use_8_DMA_buffers.patch')
conflicts=('libcrystalhd')
md5sums=('b9e2c4132a02439cff64b63152297481' '1347566a2ba0f7b8ddb0d4591c041f5e' 'e8683968b2a30ecb5eca7a3e20c11510' 'daaec53b6755ab0302e7efcd9bf1cbf3')
_gitroot='git://linuxtv.org/jarod/crystalhd.git'
_gitname='crystalhd'

package() {

    cd $startdir/src

    msg "Connecting to the GIT server...."

    if [ -d $startdir/src/$_gitname ] ; then
        cd $_gitname && git pull origin
        msg "The local files are updated."
    else
        git clone $_gitroot
        cd $_gitname
    fi

    for p in $startdir/src/*.patch
    do
      patch -p1 < "$p"
    done

    cd linux_lib/libcrystalhd

    make || return 1
    make install DESTDIR=$pkgdir || return 1
    
    mv "$pkgdir"/lib/firmware "$pkgdir"/usr/lib
    rmdir "$pkgdir"/lib

}

