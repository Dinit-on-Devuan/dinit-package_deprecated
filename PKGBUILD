## dinit init, dinitctl, dinitcheck apps #Required
## Copyright (C) 2022 Dinit on Devuan
## LISENCE: GPLv3 or later
## Originaly author: Mobin Aydinfar <mobin@mobintestserver.ir>
# Maintainer: Dinit on Devuan Project <mobin@mobintestserver.ir>

pkgname=('dinit')
pkgver=0.16.1
pkgrel=1
pkgdesc="Service monitoring / "init" system -- dinit init"

## Note: dinit should be able to work properly on any architecture supported by gcc, BUT ONLY TESTED ON amd64!
## USE IT AT YOUR OWN RISK!
#arch=(any)
arch=('amd64')

url="https://github.com/davmac314/dinit"
license=('Apache')
depends=('libc6' 'dinitscripts')
replaces=('sysvinit-core' 'runit-init' 'init' 'systemd' 'systemd-sysv' 'dinit-compat')
conflicts=('sysvinit-core' 'runit-init' 'init' 'systemd' 'systemd-sysv' 'dinit-compat')
provides=('init')

## Unfortunately makedeb does not currently support 'priority'.
## Issue #190: https://github.com/makedeb/makedeb/issues/190
#priority='required'
## Workaround #190
## https://github.com/makedeb/makedeb/issues/190#issuecomment-1179339372
control_fields=('Priority: required' 'Section: admin')

makedepends=('g++' 'make' 'm4')
source=("$url/releases/download/v$pkgver/$pkgname-$pkgver.tar.xz")

## Warning: Its checksum is only valid for 0.16.0! change it if you want newer/older version!
sha256sums=('020da31210322e01c07d30343671f6ba2b1024fab0699a1df49f390d462e8f69')

prepare(){
  cd "$srcdir"/"$pkgname-$pkgver"/configs
  chmod +x mconfig.Linux.sh
  sh ./mconfig.Linux.sh
}

build() {
  cd "$srcdir"/"$pkgname-$pkgver"/
  make DESTDIR="$pkgdir/"
}

check() {
  cd "$srcdir"/"$pkgname-$pkgver"/
  make DESTDIR="$pkgdir/" check
  make DESTDIR="$pkgdir/" check-igr
}

package() {
  cd "$srcdir"/"$pkgname-$pkgver"/
  make install DESTDIR="$pkgdir/"
  ln -s dinit "$pkgdir/sbin/init"
}
