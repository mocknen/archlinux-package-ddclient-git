# Contributor: Denton Liu <liu.denton@gmail.com>
# Contributor: Johannes Löthberg <johannes@kyriasis.com>
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Abhishek Dasgupta <abhidg@gmail.com>
# Contributor: David Rosenstrauch <darose@darose.net>

_pkgname=ddclient
pkgname=${_pkgname}-git
pkgver=v3.9.1.r313.g11a583b
pkgrel=1

pkgdesc='Update dynamic DNS entries for accounts on many dynamic DNS services'
arch=(
    'any'
)
url='https://github.com/ddclient/ddclient'
license=(
    'GPL2'
)

depends=(
    'curl'
    'iproute2'
    'perl-digest-sha1'
    'perl-io-socket-inet6'
    'perl-io-socket-ssl'
)
optdepends=(
    'smtp-forwarder: email support requires sendmail binary'
)
makedepends=(
    'git'
)
checkdepends=(
    'perl-test-mockmodule'
    'perl-test-warnings'
)

provides=(
    "${_pkgname}"
)
conflicts=(
    "${_pkgname}"
)

backup=(
    "etc/${_pkgname}/ddclient.conf"
)

_commit='11a583b003920f8e15591813598b70061d1a4654'
source=(
    "git://github.com/${_pkgname}/${_pkgname}.git#commit=${_commit}"
    "${_pkgname}.service"
)

sha512sums=(
    'SKIP'
    'a04d6976da4d49f53262dfa176ed077201aedc1e95e78ae661c49e2b4472e036507ae325533ef8051a52f86b296777ff157be754e45291653ac3618b3fa517c7'
)

pkgver() {
  cd "${_pkgname}"
  git describe --long --tags "${_commit}" | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${_pkgname}"
  ./autogen
  ./configure \
    --prefix=/usr \
    --sysconfdir="/etc/${_pkgname}" \
    --localstatedir=/var
  make
}

check() {
  cd "${_pkgname}"
  make VERBOSE=1 check
}

package() {
  install -D --mode=644 --target-directory="${pkgdir}/usr/lib/systemd/system" \
          "${_pkgname}.service"

  cd "${_pkgname}"

  make DESTDIR="${pkgdir}/" install

  install -D --mode=644 --target-directory="${pkgdir}/usr/share/doc/${_pkgname}" \
          README.cisco \
          README.md \
          README.ssl \
          sample-etc_cron.d_ddclient

  install -D --mode=644 --target-directory="${pkgdir}/usr/share/licenses/${_pkgname}" \
          COPYING \
          COPYRIGHT
}
