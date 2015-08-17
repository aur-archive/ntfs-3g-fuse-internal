# Maintainer: Gula  <gulanito.archlinux.org>

pkgname=ntfs-3g-fuse-internal
pkgver=2010.5.16
pkgrel=1
pkgdesc="Stable read and write NTFS driver (whit internal fuse suport)"
url="http://www.tuxera.com"
arch=('i686' 'x86_64')
license=('GPL2')
depends=('glibc')
optdepends=('Please, write'
'chown root $(which ntfs-3g)'
'chmod 4755 $(which ntfs-3g)'
'for user usage')
conflicts=('ntfs-3g')
makedepends=('pkgconfig')
options=('!libtool')
source=(http://www.tuxera.com/opensource/ntfs-3g-${pkgver}.tgz
        25-ntfs-config-write-policy.fdi)
sha1sums=('895da556ad974743841f743c49b734132b2a7cbc'
          '200029f2999a2c284fd30ae25734abf6459c3501')

build() {
  cd "${srcdir}/ntfs-3g-${pkgver}"
  ac_cv_path_LDCONFIG=/bin/true ./configure --prefix=/usr \
    --with-fuse=internal --disable-static || return 1
  make || return 1
}

package() {
  cd "${srcdir}/ntfs-3g-${pkgver}"
  make DESTDIR="${pkgdir}" install || return 1
  ln -s /bin/ntfs-3g "${pkgdir}/sbin/mount.ntfs" || return 1
  install -m755 -d "${pkgdir}/usr/share/hal/fdi/policy/10osvendor"
  install -m644 "${srcdir}/25-ntfs-config-write-policy.fdi" "${pkgdir}/usr/share/hal/fdi/policy/10osvendor/" || return 1
}