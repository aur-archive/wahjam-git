# Maintainer: Manuel Bärenz <manuel@enigmage.de>

pkgname=wahjam-git
pkgver=20111218
pkgrel=2
pkgdesc="A program to allow people to make real music together via the Internet; client and server; community developed version of ninjam from git"
arch=('i686' 'x86_64')
url="http://wahjam.org/"
depends=('ncurses' 'alsa-lib' 'libvorbis')
makedepends=('git' 'gcc')
license=('GPL')
provides=('wahjam-git')
replaces=('ninjam_client' 'ninjam_server')

_gitroot="https://github.com/wahjam/wahjam.git"
_gitname="wahjam"

build() {
  cd $srcdir
  msg "Connecting to the GIT server...."
  
  if [[ -d $srcdir/$_gitname ]] ; then
    cd $_gitname
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi
  
  msg "GIT checkout done"
  msg "Starting make..."
  
  cd $srcdir/$_gitname/ninjam/cursesclient
  make || return 1
  install -D -m755 cwahjam $pkgdir/usr/bin/cwahjam

  cd $srcdir/$_gitname/ninjam/server
  make || return 1
  install -D -m755 wahjamsrv $pkgdir/usr/bin/wahjamsrv
}
