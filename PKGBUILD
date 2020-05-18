# Author: Robert Maerz
pkgname=mkinitcpio-bluetooth
pkgver=1.3
pkgrel=1
pkgdesc="This is an initcpio hook for bluetooth connectivity during boot / in initramfs."
url="https://github.com/irreleph4nt/mkinitcpio-bluetooth/"
arch=('x86_64' 'i686')
license=('GPLv2')
depends=('bluez' 'bluez-utils' 'dbus')
source=('bluetooth_install' 'bluetooth_hook' 'org.bluez.conf')
md5sums=('bf5baafb0514046da7ae7411010ea31b'
	'b5e9f304ad0e1b6ac56d7a22d22f0b3a'
	'5c171037726256d674bcc2d05fdbab86'
)

package() {
	install -Dm644 bluetooth_install "${pkgdir}/usr/lib/initcpio/install/bluetooth"
	install -Dm644 bluetooth_hook "${pkgdir}/usr/lib/initcpio/hooks/bluetooth"
	install -Dm644 org.bluez.conf "${pkgdir}/usr/lib/initcpio/bluetooth/org.bluez.conf"
}

# vim:set ts=2 sw=2 et:
