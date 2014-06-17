# Maintainer: Aurélien DESBRIÈRES <aurelien@hackers.camp>

pkgname=mkinitcpio-paralogo
pkgver=0.0.1
pkgrel=1
pkgdesc="Add colored Parabola Linux ASCII art logo to early boot process"
arch=('any')
url="https://github.com/XL04D/mkinitcpio-paralogo"
depends=('mkinitcpio')
makedepends=('git')
license=('GPL')
install=mkinitcpio-paralogo.install
source=('git://github.com/XL04D/mkinitcpio-paralogo.git')
backup=('etc/paralogo.conf')
    
pkgver() {
	cd mkinitcpio-paralogo/

	if GITTAG="$(git describe --abbrev=0 --tags 2>/dev/null)"; then
		echo "$(sed -e "s/^${pkgname%%-git}//" -e 's/^[-_/a-zA-Z]\+//' -e 's/[-_+]/./g' <<< ${GITTAG}).r$(git rev-list --count ${GITTAG}..).g$(git log -1 --format="%h")"
	else
		echo "0.r$(git rev-list --count master).g$(git log -1 --format="%h")"
	fi
}

package() {
	cd mkinitcpio-paralogo/

	# install install script and unit file
	install -D -m0644 install/paralogo ${pkgdir}/usr/lib/initcpio/install/paralogo
	install -D -m0644 systemd/paralogo.service ${pkgdir}/usr/lib/systemd/system/paralogo.service

	# install hook for plain old script based initramfs
	install -D -m0755 hook/paralogo ${pkgdir}/usr/lib/initcpio/hooks/paralogo

	# install config
	install -D -m0644 etc/paralogo.conf ${pkgdir}/etc/paralogo.conf

	# install logos
	install -D -m0644 share/paralogo ${pkgdir}/usr/share/paralogo/paralogo
	install -D -m0644 share/paralogo2 ${pkgdir}/usr/share/paralogo/paralogo2
}

sha256sums=('SKIP')
