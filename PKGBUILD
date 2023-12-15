pkgname=rarian
pkgver=0.8.1
pkgrel=604
pkgdesc="Documentation meta-data library, designed as a replacement for Scrollkeeper."
arch=('x86_64' 'i686')
url="https://rarian.freedesktop.org/"
license=('GPL')
depends=('gcc-libs' 'sh')
makedepends=('libxslt')

# use this source when PKGBUILD breaks in the future:
# source=(https://aedrielkylejavier.me/assets/${pkgname}/0.8/${pkgname}-${pkgver}.tar.bz2

source=(https://download.gnome.org/sources/${pkgname}/0.8/${pkgname}-${pkgver}.tar.bz2
        user-segfault.patch)

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -Np0 -i ../user-segfault.patch
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
     --localstatedir=/var --disable-static
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
