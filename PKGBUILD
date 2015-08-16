# Contributor: Adria Arrufat <swiftscythe@gmail.com>

pkgname=lyx-svn
pkgver=40284
pkgrel=1
pkgdesc="An advanced open-source document processor."
arch=(i686 x86_64)
url='http://www.lyx.org'
depends=('qt' 'texlive-core' 'python' 'perl' 'imagemagick' 'aspell' 'aiksaurus' 'boost')
optdepends=('texlive-latex3: pdf export')
makedepends=('bc' 'cmake' 'subversion')
license=('GPL')
source=('lyx.desktop' 'lyx.png')
md5sums=('c11db315dc99254a4118827f98922623'
         'fcbfb9c9d4716f69ae8c64cf13e9a6fb')

_svntrunk=svn://svn.lyx.org/lyx/lyx-devel/trunk
_svnmod=lyx

build() {
  svn co $_svntrunk $_svnmod

  msg "SVN checkout done or server timeout"
  msg "Starting make..."
  export PYTHON=python2
  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build/
    ./autogen.sh
    ./configure --prefix=/usr \
    --with-frontend=qt4 --enable-build-type=release
  make || return 1
  make -j 2 DESTDIR=${pkgdir} install || return 1

  # install desktop entry
  install -Dm644 ${srcdir}/lyx.desktop \
	${pkgdir}/usr/share/applications/lyx.desktop || return 1
  cp ${srcdir}/lyx.png ${pkgdir}/usr/share/lyx/images/lyx.png
}
