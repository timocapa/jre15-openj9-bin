# Maintainer: Davide Depau <davide@depau.eu>
# Contributor: Mohammadreza Abdollahzadeh <morealaz at gmail dot com>

pkgname=jre15-openj9-bin
_jdkver=15
_openj9ver=0.24.0
_majorver=${_jdkver}.0.2
_buildvershort=7
_buildver=${_buildvershort}_openj9-${_openj9ver}
pkgver=${_majorver}b${_buildver//-/_}
pkgrel=1
pkgdesc="Eclipse (former IBM) OpenJ9 with openjdk${_jdkver}"
arch=('x86_64')
url="https://adoptopenjdk.net/index.html?variant=openjdk${_jdkver}&jvmVariant=openj9"
license=('GPL2')
depends=('java-environment-common' 'ca-certificates-utils' 'nss')
provides=(
  "java-environment=${_jdkver}"
  "java-environment-openjdk=${_jdkver}"
  "java-runtime=${_jdkver}"
  "java-runtime-openjdk=${_jdkver}"
  "java-runtime-headless=${_jdkver}"
  "java-runtime-headless-openjdk=${_jdkver}"
)
options=(!strip)
source=("https://github.com/AdoptOpenJDK/openjdk${_jdkver}-binaries/releases/download/jdk-${_majorver}%2B${_buildver}/OpenJDK${_jdkver}U-jre_x64_linux_openj9_${_majorver}_${_buildver}.tar.gz")
sha256sums=('a4ae1b7275fcfd6d87a3387edacc8e353dc95ee44f00ca5a348ea90331ec2084')

_jvmdir=usr/lib/jvm/java-${_jdkver}-j9

package() {
  # Install
  install -d "${pkgdir}/${_jvmdir}"
  cd jdk-${_majorver}+${_buildvershort}-jre
  cp -a bin lib release "${pkgdir}/${_jvmdir}/"
  # Link JKS keystore from ca-certificates-utils
  rm -f "${pkgdir}/${_jvmdir}/lib/security/cacerts"
  # Legal
  install -d "${pkgdir}/usr/share/licenses/java${_jdkver}-j9"
  cp -a legal "${pkgdir}/usr/share/licenses/java${_jdkver}-j9/"
  ln -s /usr/share/licenses/java${_jdkver}-j9 "${pkgdir}/${_jvmdir}/legal"
  # Conf
  install -d "${pkgdir}/etc"
  cp -r conf "${pkgdir}/etc/java${_jdkver}-j9"
  ln -s /etc/java${_jdkver}-j9 "${pkgdir}/${_jvmdir}/conf"
  ln -s /usr/share/man "${pkgdir}/${_jvmdir}/man"
}
# vim:set ts=2 sw=2 et:
