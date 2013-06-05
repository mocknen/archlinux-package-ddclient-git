# $Id$
# Maintainer: Jonathan Steel <mail@jsteel.org>
# Contributor: Abhishek Dasgupta <abhidg@gmail.com>
# Contributor: David Rosenstrauch <darose@darose.net>

pkgname=ddclient
pkgver=3.8.1
pkgrel=8
pkgdesc="Update dynamic DNS entries for accounts on many dynamic DNS services"
arch=('any')
url="http://ddclient.sourceforge.net"
license=('GPL2')
depends=('perl-io-socket-ssl' 'perl-digest-sha1')
backup=('etc/ddclient/ddclient.conf')
install=ddclient.install
source=(http://downloads.sourceforge.net/sourceforge/$pkgname/$pkgname-$pkgver.tar.bz2
        ddclient.service
        iproute2.patch
        usrbin.patch)
md5sums=('7fa417bc65f8f0e6ce78418a4f631988'
         '3a31ec40ac583779fd049b1930f4af9f'
         'e0c8a07e9b7a69e73cecd8626f16e8f0'
         '65e294485a18b8d3f752a124913579f1')

build() {
  cd "$srcdir"/ddclient-$pkgver

  patch -p1 < "$srcdir"/iproute2.patch
  patch -Np0 -i "$srcdir"/usrbin.patch
}

package() {
  cd "$srcdir"/ddclient-$pkgver

  # core files
  install -Dm755 ddclient "$pkgdir"/usr/bin/ddclient
  install -Dm600 sample-etc_ddclient.conf "$pkgdir"/etc/ddclient/ddclient.conf
  install -d "$pkgdir"/var/cache/ddclient

  # additional instructions, sample configs
  install -Dm644 README "$pkgdir"/etc/ddclient/samples/README
  install -Dm644 sample-etc_cron.d_ddclient "$pkgdir"/etc/ddclient/samples/sample-etc_cron.d_ddclient
  install -Dm644 sample-etc_dhcpc_dhcpcd-eth0.exe "$pkgdir"/etc/ddclient/samples/sample-etc_dhcpc_dhcpcd-eth0.exe
  install -Dm644 sample-etc_ppp_ip-up.local "$pkgdir"/etc/ddclient/samples/sample-etc_ppp_ip-up.local
  install -Dm644 "$srcdir"/$pkgname.service "$pkgdir"/usr/lib/systemd/system/$pkgname.service
}
