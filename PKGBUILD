# Maintainer: dr460nf1r3 <dr460nf1r3 at persianosxlinux dot org>
# Contributor: Philip Müller <philm[at]persianosx[dog]org>
# Contributor: artoo <artoo@persianosx.org>
# Contributor: anex <assassin.anex[@]gmail.com>

_repo=persianosx-tools-livedisk

pkgbase=persianosx-live
pkgname=('persianosx-live-base'
	'persianosx-live-systemd'
	'persianosx-live-skel'
	'persianosx-live-portable-efi')
pkgver=r5.a80f397
pkgrel=1
pkgdesc='PersianOSX live session'
arch=('any')
url="https://github.com/p30developer/persianosx-tools-livedisk"
license=('GPL')
makedepends=('git')
source=("git+$url.git")
sha256sums=('SKIP')

pkgver() {
	cd "${srcdir}"/persianosx-tools-livedisk || exit
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "${srcdir}"/${_repo} || exit #-${pkgver}
	make PREFIX=/usr SYSCONFDIR=/etc
}

package_persianosx-live-base() {
	pkgdesc='PersianOSX live base scripts'
	depends=('persianosx-tools-base>=0.13')
	conflicts=('persianosx-livecd-base')
	replaces=('persianosx-livecd-base')

	cd "${srcdir}"/${_repo} || exit #-${pkgver}
	make PREFIX=/usr SYSCONFDIR=/etc DESTDIR="${pkgdir}" install_base
}

package_persianosx-live-systemd() {
	pkgdesc='PersianOSX live Systemd units'
	depends=('systemd' 'persianosx-live-base' 'reflector')
	conflicts=('persianosx-livecd-systemd')
	# 	replaces=('persianosx-livecd-systemd')

	cd "${srcdir}"/${_repo} || exit #-${pkgver}
	make PREFIX=/usr SYSCONFDIR=/etc DESTDIR="${pkgdir}" install_sd
}

package_persianosx-live-skel() {
	pkgdesc='PersianOSX live session autostart items'

	cd "${srcdir}"/${_repo} || exit #-${pkgver}
	make PREFIX=/usr SYSCONFDIR=/etc DESTDIR="${pkgdir}" install_xdg
}

package_persianosx-live-portable-efi() {
	pkgdesc='PersianOSX live session portable EFI settings'
	depends=('grub')

	cd "${srcdir}"/${_repo} || exit #-${pkgver}
	make PREFIX=/usr SYSCONFDIR=/etc DESTDIR="${pkgdir}" install_portable_efi
}
