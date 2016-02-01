# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Alexander Duscheleit <jinks@archlinux.us>

pkgbase=python-colorama
pkgname=('python-colorama' 'python2-colorama')
pkgver=0.3.6
pkgrel=1
pkgdesc="Python API for cross-platform colored terminal text."
arch=('any')
url="http://pypi.python.org/pypi/colorama"
license=('BSD')
makedepends=('python-setuptools' 'python2-setuptools' 'git')
checkdepends=('python-mock' 'python2-mock')
source=("git+https://github.com/tartley/colorama.git#tag=$pkgver"
        wrapped.patch)
md5sums=('SKIP'
         '5845be5ce4ac50b5e74c4ca44424e669')

prepare() {
  # https://github.com/tartley/colorama/pull/84
  (cd colorama; patch -p1 -i ../wrapped.patch)
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
