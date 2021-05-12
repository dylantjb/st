pkgname=st-dylan-git
_pkgname=st-dylan
pkgver=0.8.4.r1132.8090053
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='https://github.com/dylantjb/st.git'
arch=('i686' 'x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
makedepends=('ncurses' 'libxext' 'git')
optdepends=('dmenu' 'xclip')

source=("${_pkgname}::git+$url")
sha256sums=('SKIP')
provides=('st')
conflicts=('st')

pkgver() {
  cd "${_pkgname}"
  _pkgver=$(awk '/VERSION/ {print $3}' config.mk|head -1)
  echo "${_pkgver}.r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${_pkgname}"
  sed -i '/tic /d' Makefile
}

build() {
  cd "${_pkgname}"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "${_pkgname}"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
