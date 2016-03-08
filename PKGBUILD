# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Alexander Duscheleit <jinks@archlinux.us>

pkgbase=python-colorama
pkgname=('python-colorama' 'python2-colorama')
pkgver=0.3.7
_commit=9f5a28369c4528502b9faa76088df965f6ac103d
pkgrel=1
pkgdesc="Python API for cross-platform colored terminal text."
arch=('any')
url="http://pypi.python.org/pypi/colorama"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools' 'git')
checkdepends=('python-mock' 'python2-mock')
source=("git+https://github.com/tartley/colorama.git#commit=$_commit")
md5sums=('SKIP')

prepare() {
  cp -a colorama{,-py2}
}

build() {
  cd "$srcdir/colorama"
  python setup.py build

  cd "$srcdir/colorama-py2"
  python2 setup.py build
}

check() {
  cd "$srcdir/colorama"
  python -m unittest discover -p *_test.py || warning "Tests failed"

  cd "$srcdir/colorama-py2"
  python2 -m unittest discover -p *_test.py || warning "Tests failed"
}

package_python-colorama() {
  depends=('python')

  cd "$srcdir/colorama"
  python setup.py install --root="$pkgdir" --optimize=1

  install -Dm644 LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"
}

package_python2-colorama() {
  depends=('python2')

  cd "$srcdir/colorama-py2"
  python2 setup.py install --root="$pkgdir" --optimize=1

  install -Dm644 LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"
}

# vim:set ts=2 sw=2 et:
