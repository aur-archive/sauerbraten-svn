# Maintainer: archtux <antonio.arias99999@gmail.com>
# Contributer: giacomogiorgianni@gmail.com 

pkgname=sauerbraten-svn
pkgver=4365
pkgrel=1
pkgdesc="Free multiplayer/singleplayer FPS, built as a major redesign of the Cube FPS"
url="http://sauerbraten.org/"
depends=('libgl' 'sdl_image' 'sdl_mixer')
makedepends=('subversion')
arch=('i686' 'x86_64')
license=('ZLIB')

_svntrunk=https://sauerbraten.svn.sourceforge.net/svnroot/sauerbraten
_svnmod=sauerbraten

build() {
  cd $srcdir
   
  svn checkout $_svntrunk --config-dir ./ -r $pkgver $_svnmod

  msg "SVN checkout done or server timeout"
  msg "Starting make..."
}
  package() {

  cd $srcdir/sauerbraten/src
  make 
  cd $srcdir/sauerbraten
  #make DESTDIR="${pkgdir}" install
  mkdir -p "${pkgdir}/usr/share/"  "${pkgdir}/usr/share/sauerbraten-svn/"
  
  cp sauerbraten_unix server-init.cfg $pkgdir/usr/share/sauerbraten-svn
  cp -R bin_unix/ data/ packages/ $pkgdir/usr/share/sauerbraten-svn

  # Start file
  install -Dm755 $srcdir/sauerbraten/sauerbraten_unix $pkgdir/usr/bin/sauerbraten-svn
  install -D $srcdir/sauerbraten/src/sauer_client $pkgdir/usr/bin/
  install -D $srcdir/sauerbraten/src/sauer_server $pkgdir/usr/bin/
  # Desktop icon
  #install -Dm644 data/cube.png $pkgdir/usr/share/pixmaps/sauerbraten-svn.png
  #install -Dm644 $startdir/sauerbraten-svn.desktop $pkgdir/usr/share/applications/sauerbraten-svn.desktop

  # License
  #install -Dm644 $srcdir/readme_source.txt $pkgdir/usr/share/licenses/sauerbraten-svn/LICENSE

  # Remove unneeded files
  cd $pkgdir/usr/share/sauerbraten-svn
  rm -rf bin_unix/.svn
  rm -rf data/.svn
  rm -rf packages/.svn

  cd bin_unix
  if [ "${CARCH}" = 'x86_64' ]; then
  rm linux_client linux_server
    elif  [ "${CARCH}" = 'i686' ]; then 
  rm linux_64_client linux_64_server
  fi
}