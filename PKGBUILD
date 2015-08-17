# Maintainer: Alejandro Perez <alejandro.perez.mendez@gmail.com>

pkgbase=tracker
pkgname=(tracker-needle-configurable)
pkgver=0.16.1
_tver=${pkgver%.*}
pkgrel=2
pkgdesc="Modification of tracker-needle to allow several configuration options in command line (limit of results, quick results, exit after launch). Intended for be used as a quick way to find files and open them (like the tracker search in gnome-shell overview)"
arch=(i686 x86_64)
license=(GPL)
makedepends=(libgee libsecret upower libexif exempi
             poppler-glib libgsf icu enca networkmanager gtk3
             desktop-file-utils hicolor-icon-theme gobject-introspection
             intltool giflib gst-plugins-base-libs totem-plparser
             taglib libvorbis flac vala libgxps libnautilus-extension)
url="http://www.gnome.org"
options=('!libtool' '!emptydirs')
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgbase/$_tver/$pkgbase-$pkgver.tar.xz tracker-needle-configurable.patch)
sha256sums=('fbb94144826b00da0b427dc6f37d2679bd8dfec1dc992e857a47a0b453f0b771'
            '1244134c1b2b2072fd3b74e7dada1ffe2760800c7085e0587ba202ed19e6bc51')

build() {
  cd $pkgbase-$pkgver
  patch -Np0 -i ../tracker-needle-configurable.patch
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/tracker \
    --disable-unit-tests \
    --enable-libflac \
    --enable-libvorbis

  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0 /g' -e 's/    if test "$export_dynamic" = yes && test -n "$export_dynamic_flag_spec"; then/      func_append compile_command " -Wl,-O1,--as-needed"\n      func_append finalize_command " -Wl,-O1,--as-needed"\n\0/' libtool

  make
}

package() {
  depends=("libtracker-sparql=$pkgver-1" libgee libsecret
           upower libexif exempi poppler-glib libgsf enca
           networkmanager gtk3 desktop-file-utils hicolor-icon-theme)

  mkdir -p $pkgdir/usr/bin/
  cp $pkgbase-$pkgver/src/tracker-needle/.libs/tracker-needle $pkgdir/usr/bin/tracker-needle-configurable
}
