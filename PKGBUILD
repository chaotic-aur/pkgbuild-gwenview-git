# Maintainer: Antonio Rojas <arojas@archlinux.org>

pkgname=gwenview-git
pkgver=r6849.8cc4c78c
pkgrel=1
pkgdesc='A fast and easy to use image viewer for KDE'
arch=('i686' 'x86_64')
url='http://kde.org/applications/graphics/gwenview/'
license=('GPL')
depends=('kactivities-git' 'kdelibs4support' 'exiv2' 'libkdcraw-git' 'libkipi-git' 'phonon-qt5-git')
makedepends=('extra-cmake-modules' 'git' 'kdoctools' 'python')
conflicts=('kdegraphics-gwenview' 'gwenview')
provides=('gwenview')
source=("git+https://invent.kde.org/graphics/gwenview.git")
install=$pkgname.install
sha256sums=('SKIP')

#pkgver() {
#  cd gwenview
#  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
#}

pkgver() {
  cd ${srcdir}/${pkgname%-git}
  _ver="$(cat CMakeLists.txt | grep RELEASE_SERVICE_VERSION | cut -d '"' -f2 | tr '\n' '.' | cut -d "." -f 1-3)"
  echo "$(echo ${_ver}).r$(git rev-list --count HEAD)"
}

prepare() {
  mkdir -p build
}

build() { 
  cd build
  cmake ../gwenview \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DLIB_INSTALL_DIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
