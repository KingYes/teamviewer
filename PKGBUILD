# Maintainer: Yakir Sitbon <kingyes1 at gmail dot com>
# Contributor: Alucryd <alucryd at gmail dot com>
# Contributor: Stas S <whats_up at tut dot by>
# Contributor: Hilinus <itahilinus at hotmail dot it>

pkgname=teamviewer
pkgver=10.0.36281
pkgrel=1
pkgdesc="All-In-One Software for Remote Support and Online Meetings"
arch=('i686' 'x86_64')
url="http://www.teamviewer.com"
license=('custom')
depends=('bash')
options=('!strip')
install=${pkgname}.install

if [[ $CARCH == 'i686' ]]; then
  source=("teamviewer_linux-${pkgver}.deb::http://download.teamviewer.com/download/teamviewer_i386.deb")
  md5sums=('d87cb34d21595a5bc3f9906f28f92c31')
  depends+=('alsa-lib' 'gcc-libs' 'libxdamage' 'libxtst' 'zlib' 'freetype2' 'libxrandr')
elif [[ $CARCH == 'x86_64' ]]; then
  source=("teamviewer_linux_x64-${pkgver}.deb::http://download.teamviewer.com/download/teamviewer_amd64.deb")
  md5sums=('c702eec31351096fda56fdef9f1e4916')
  depends+=('lib32-gcc-libs' 'lib32-alsa-lib' 'lib32-libxtst' 'lib32-libxdamage' 'lib32-zlib' 'lib32-freetype2' 'lib32-libxrandr')
fi

build() {
  cd "${srcdir}"
  tar -xf data.tar.gz
}

package() {
  cd "${srcdir}"

# Install
  cp -dr --no-preserve=ownership {etc,opt,usr,var} "${pkgdir}"/

# Additional files
  rm "${pkgdir}"/opt/teamviewer/tv_bin/xdg-utils/xdg-email
  install -dm 755 "${pkgdir}"/usr/{lib/systemd/system,share/applications,share/licenses/teamviewer}
  install -m 644 "${pkgdir}"/opt/teamviewer/tv_bin/script/teamviewerd.service "${pkgdir}"/usr/lib/systemd/system/teamviewerd.service
  ln -s /opt/teamviewer/tv_bin/desktop/teamviewer-teamviewer.desktop "${pkgdir}"/usr/share/applications/teamviewer.desktop
  ln -s /opt/teamviewer/License.txt "${pkgdir}"/usr/share/licenses/teamviewer/LICENSE
}

