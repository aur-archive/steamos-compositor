# Maintainer: Christoph Haag <haagch@studi,informatik.uni-stuttgart.de>
# Contributor: WorMzy Tykashi <wormzy.tykashi@gmail.com>
pkgname=steamos-compositor
pkgver=1.24
pkgrel=1
pkgdesc="Compositor used by SteamOS \"based on xcompmgr by Keith Packard et al.\""
arch=('i686' 'x86_64')
url="http://repo.steampowered.com/steamos/pool/main/s/steamos-compositor/"
license=('GPL')
depends=('libxfixes' 'libxext' 'libxcomposite' 'libxdamage' 'libxrender' 'libxxf86vm' 'sdl_image' 'libgl')
makedepends=('mesa' 'libxt' 'libxpm' 'lesstif') # 'openmotif') 
source=("http://repo.steampowered.com/steamos/pool/main/s/steamos-compositor/steamos-compositor_${pkgver}.tar.xz")

prepare() {
  cd "$srcdir/$pkgname"
  rm -rf autom4te.cache aclocal.m4 configure
  autoreconf -i

#https://bugs.freedesktop.org/show_bug.cgi?id=83631
cd src
sed -i '/#include <X11\/Xatom.h>/a typedef ptrdiff_t GLsizeiptr;' steamcompmgr.c
sed -i '/typedef ptrdiff_t GLsizeiptr;/a typedef ptrdiff_t GLintptr;' steamcompmgr.c
}

build() {
  export LIBS="-lXm -lXext -lXt -lXpm -lXdamage -lXfixes"
  cd "$srcdir/$pkgname"
  ./configure --prefix=/usr
  make
}

check() {
  cd "$srcdir/$pkgname"
  make -k check
}

package() {
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir/" install
  cp -ra usr "$pkgdir/"
chmod +x "$pkgdir"/usr/bin/steamos-session
}

md5sums=('c9255936da3a28651b22b38ab0e58a9e')
