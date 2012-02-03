# Contributor: Guten <ywzhaifei@gmail.com>

pkgname=user-daemon-system-git
pkgver=20120203  
pkgrel=1
pkgdesc="A User based Daemon System for ZSH. READ https://github.com/GutenYe/user-daemon-system FIRST." 
arch=("i686" "x86_64")
url="https://github.com/GutenYe/user-daemon-system"
license=("MIT-LICENSE")
groups=()
depends=("zsh")
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=("home/$USER/etc/rc.conf")
options=()
changelog=

_gitroot="git://github.com/GutenYe/user-daemon-system"
_gitname="user-daemon-system"

build1() {
  cd ${srcdir}
  msg "Connecting to GIT server...."

  if [ -d ${_gitname}/.git ] ; then
    cd ${_gitname}

    # Change remote url to anongit
    if [ -z $( git branch -v | grep anongit ) ] ; then
        git remote set-url origin ${_gitroot}
    fi
    
    git pull origin
    msg "The local files are updated."
  else
    git clone ${_gitroot} ${_gitname}
  fi
  msg "GIT checkout done or server timeout"
}

package() {
  p_root="$pkgdir/home/$USER"
  cd $srcdir/$_gitname

  mkdir -p $p_root
  cp -r etc $p_root
  mkdir -p $p_root/var/run/daemons
  mkdir -p $p_root/var/cache
  mkdir -p $p_root/var/log
  mkdir -p $p_root/etc/conf.d
  mkdir -p $p_root/etc/rc.d/functions.d

  chown $USER:$USER -R $pkgdir

  mkdir -p $pkgdir/usr/bin
  cp bin/user-daemon-system $pkgdir/usr/bin
}


# vim:set ts=2 sw=2 et:
