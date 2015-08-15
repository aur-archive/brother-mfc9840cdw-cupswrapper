# Contributor:Gero Mueller <gero.mueller (at) cloo (dot) de>
pkgname=brother-mfc9840cdw-cupswrapper
_printer=mfc9840cdw  # note: Should be changed to lowercase if used.
                   #       Currently uppercase to match .deb filename
pkgver=1.0.2_4
pkgrel=1
pkgdesc="LPR-to-CUPS wrapper for Brother MFC-9840CDW multifunction network printer"
arch=('i686' 'x86_64')
url="http://solutions.brother.com/linux/en_us/download_prn.html#MFC-9840CDW"
license=('custom:Brother_Software_Open_License_Agreement')
depends=('cups' 'ghostscript' 'brother-mfc9840cdw-lpr>=1.0.2_4')
makedepends=('binutils')
provides=("$pkgname=${pkgver%_*}")
conflicts=("$pkgname")
replaces=("$pkgname")
install="$pkgname.install"
source=('http://solutions.brother.com/Library/sol/printer/linux/dlf/mfc9840cdwcupswrapper-1.0.2-4.i386.deb'
        'license.txt')
build() {
  cd $srcdir

  # extract the archive
  ar x mfc9840cdwcupswrapper-1.0.2-4.i386.deb || return 1
  mkdir data
  tar -xzvf data.tar.gz -C data || return 1

  # correct the directory structure
  mv data/usr/local/Brother data/usr/share/brother
  rm -r data/usr/local
  sed -i 's|/usr/local/Brother|/usr/share/brother|g' `grep -lr '/usr/local/Brother' data/` || return 1
  sed -i 's|/etc/init.d|/etc/rc.d|' "data/usr/share/brother/Printer/mfc9840cdw/cupswrapper/cupswrapperSetup_mfc9840cdw" || return 1

  # copy into place
  cp -r data/usr $pkgdir || return 1

  # install the license
  install -D -m644 license.txt $pkgdir/usr/share/licenses/$pkgname/license.txt || return 1
}

# vim:set ts=2 sw=2 et:
