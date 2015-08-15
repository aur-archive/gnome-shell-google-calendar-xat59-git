# Maintainer:  Gen2ly             <toddrpartridge@gmail.com>
# Contributor: Daniel Apolinario  <dapolinario@gmail.com>
# Contributor: Pietro Bonfa       <bonfus at gmail com>
# Submitter:   pie86

pkgname=gnome-shell-google-calendar-xat59-git
_pkgname=gnome-shell-google-calendar
pkgver=20120630
pkgrel=1
pkgdesc="GNOME shell calendar integration with Google Calendar (xat59 fork)"
arch=('any')
url="https://github.com/Xat59/gnome-shell-google-calendar"
license=('GPL')
makedepends=('git')
depends=('dbus-python' 'gnome-shell' 'pygtk' 'python2-iso8601' 'python-gdata' 'python-gnomekeyring')
conflicts=('gnome-shell-google-calendar-git')
install="${pkgname}.install"
source=("${_pkgname}.desktop"
        "${_pkgname}.sh")
md5sums=('087fdd94b703243c652f83968dc2d2de'
         '5b6432164848d7bebbe206c38e4c6074')

_gitroot="git://github.com/Xat59/gnome-shell-google-calendar"
_gitname="gnome-shell-google-calendar"

build() {

  cd "$srcdir/"

  msg "Connecting to GIT server..."
  if [ -d $_gitname ]; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone --depth=1 $_gitroot $_gitname
  fi
  msg "GIT checkout done or server timeout"

}

package() {

  # Create pkgdirs, enter source directory
  _pkgshr="${pkgdir}/usr/share/gnome-shell-google-calendar/"
  _pkgbin="${pkgdir}/usr/bin/"
  mkdir -p "$_pkgshr"
  mkdir -p "$_pkgbin"
  cd "$srcdir/${_gitname}"

  # Install python files
  install -Dm 0755 "gnome-shell-google-calendar.py" "$_pkgshr"
  install -Dm 0755 "keyring.py"                     "$_pkgshr"

  # Install start script
  install -Dm 0755 "${srcdir}/${_pkgname}.sh"       "$_pkgbin"$_pkgname

  # Install autostart launcher
  install -Dm 0644 "${srcdir}/${_pkgname}.desktop"  "$_pkgshr"

  # Patch python script for python2
  sed -i 's/env python$/env python2/' "$_pkgshr"gnome-shell-google-calendar.py
  msg "Patched python script to python version 2"

}

# vim:set ts=2 sw=2 et: