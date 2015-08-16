# Maintainer: Mikael Eriksson <mikael_eriksson@miffe.org>

pkgname=mingw32-libpng14
pkgver=1.4.12
pkgrel=2
arch=('any')
pkgdesc="A collection of routines used to create PNG format graphics (mingw32)"
depends=('mingw32-runtime' 'mingw32-zlib')
makedepends=('mingw32-gcc')
license=('custom')
url="http://www.libpng.org/pub/png/libpng.html"
options=(!strip !buildflags staticlibs)
provides=(mingw32-libpng)
conflicts=(mingw32-libpng)
source=("http://downloads.sourceforge.net/sourceforge/libpng/libpng-$pkgver.tar.bz2"
        "http://downloads.sourceforge.net/sourceforge/libpng-apng/libpng14/$pkgver/libpng-$pkgver-apng.patch.gz")
md5sums=('849b14d88e1240a1b9f2cb39dd39701e'
         'ab812e0f8ef70588d9168a0d84c13cd8')

build() {
  cd "$srcdir/libpng-$pkgver"

  # Add animated PNG (apng) support
  # see http://sourceforge.net/projects/libpng-apng/
  patch -p1 -i "${srcdir}/libpng-$pkgver-apng.patch" || return 1

  ./configure --host=i486-mingw32 --prefix=/usr/i486-mingw32
  #make -f scripts/makefile.mingw \
    #CC=i486-mingw32-gcc \
    #LD=i486-mingw32-ld \
    #AR=i486-mingw32-ar \
    #RANLIB=i486-mingw32-ranlib \
    #prefix=/usr/i486-mingw32 \
    #DESTDIR=$pkgdir \
    #install

  make
}

package() {
  cd "$srcdir/libpng-$pkgver"
  make install DESTDIR=$pkgdir

  install -D -m644 LICENSE "$pkgdir/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
