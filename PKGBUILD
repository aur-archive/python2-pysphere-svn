# Maintainer: Josh VanderLinden <arch@cloudlery.com>
pkgname=python2-pysphere-svn
pkgver=89
pkgrel=1
pkgdesc="vSphere SDK for Python"
arch=('any')
url="https://code.google.com/p/pysphere/"
license=('BSD')
depends=('python2')
makedepends=('subversion' 'python2')
provides=('pysphere')
source=('issue_16.patch')
md5sums=('b2ad650cce9b590e2a3a12ffcc32ad19')

_svntrunk=http://pysphere.googlecode.com/svn/trunk/
_svnmod=pysphere

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  msg "Patching code to handle a UnicodeDecodeError"
  patch -Np2 --binary -i ../../issue_16.patch
}

package() {
  cd "$srcdir/$_svnmod-build"
  python2 setup.py install --root="${pkgdir}/" --optimize=1
}

# vim:set ts=2 sw=2 et: