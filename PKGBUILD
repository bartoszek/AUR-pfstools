# Maintainer: Lukas Jirkovsky <l.jirkovsky@gmail.com>
# Contributor: Brandon Andrews <bsa@bsa.isa-geek.com>
# Contributor: Mael Kerbiriou <mael.kerbiriouATfreeDOTfr>
pkgname=pfstools
pkgver=2.1.0
pkgrel=2
pkgdesc="Set of command line programs for reading, writing and manipulating high-dynamic range (HDR) images"
arch=('i686' 'x86_64')
url="http://pfstools.sourceforge.net/"
license=('LGPL2.1')
depends=('gcc-libs')
provides=('pfscalibration' 'pfstmo')
conflicts=('pfscalibration' 'pfstmo')
optdepends=('freeglut: OpenGL image viewer pfsglview' 'glu: OpenGL image viewer pfsglview' \
            'opencv: pfsalign' 'gtk3: pfsalign' \
            'openexr: OpenEXR support' \
            'imagemagick: ImageMagick support' \
            'netpbm: PBM support' \
            'dcraw: RAW support' \
            'gsl: mantiuk08 tone mapping operator' \
            'fftw: durand02,fattal02,ferradans11 tone mapping operators')
makedepends=('cmake' \
             'openexr' 'libmagick6' 'libtiff' 'netpbm' \
             'gsl' 'fftw' 'libexif' 'opencv'
             'freeglut' 'glu' 'gtkglext' 'gtk3')
options=(!libtool)
source=("http://downloads.sourceforge.net/pfstools/$pkgname-$pkgver.tgz"
        "opencv3.patch" "force_imagemagick6.patch")
sha256sums=('3dea4248e41bf433fe4760b0a11d138ad2d240f62db9e519bcb1d557c0593413'
            '2933635f5b5be07fcede7c90baaad533cbbb87aa0e8bb8add530652da595bad6'
            'ab98716861280299d964496b3a3c35bb873d828060e353a4906efb465aba4674')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

  patch -Np1 < "$srcdir/opencv3.patch"
  patch -Np1 < "$srcdir/force_imagemagick6.patch"
}

build() {
  mkdir -p "$srcdir/build"
  cd "$srcdir/build"

  cmake "$srcdir/$pkgname-$pkgver" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DWITH_Octave=OFF # disable octave, as it breaks build

  make
}

package() {
  cd "$srcdir/build"
  make DESTDIR="$pkgdir/" install
}
