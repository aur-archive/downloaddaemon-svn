# Contributor: Danilo T. <tillocad@libero.it>
# ------------------------------------------
# Build: daemon, ddconsole
 
pkgname=downloaddaemon-svn
pkgver=1334
pkgrel=1
pkgdesc="Download Manager for Special Hosters (rapidshare.com/megaupload.com/youtube.com/...)"
arch=('i686' 'x86_64' 'arm')
url="http://downloaddaemon.sourceforge.net/"
license=('GPL')
depends=('curl' 'gcc-libs' 'glibc' 'boost')
backup=('etc/downloaddaemon/downloaddaemon.conf' 'etc/downloaddaemon/premium_accounts.conf' 'etc/downloaddaemon/routerinfo.conf')
conflicts=('downloaddaemon')
makedepends=('subversion' 'cmake')

_svntrunk="svn://svn.code.sf.net/p/downloaddaemon/code/trunk"
_svnmod="downloaddaemon-code"

build() {

cd $startdir/src
mkdir -p ~/.subversion

svn co $_svntrunk $_svnmod
msg "SVN checkout done or server timeout"

msg "Starting make: ddconsole..."
cd "$srcdir/$_svnmod/src/ddconsole"
cmake . -DCMAKE_INSTALL_PREFIX=/usr -DUSE_STD_THREAD=0 -DCMAKE_CXX_LINK_FLAGS:STRING="-lboost_system"

msg "Starting make: daemon..."
cd "$srcdir/$_svnmod/src/daemon"
cmake . -DCMAKE_INSTALL_PREFIX=/usr -DUSE_STD_THREAD=0 -DCMAKE_CXX_LINK_FLAGS:STRING="-lboost_system"

}

package() {

  msg "Build: ddconsole..." 
  cd "$srcdir/$_svnmod/src/ddconsole"
  make DESTDIR=${pkgdir} install

  msg "Build: daemon..."
  cd "$srcdir/$_svnmod/src/daemon"
  make DESTDIR=${pkgdir} install

}

