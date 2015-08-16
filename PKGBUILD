# Maintainer : Robin Hahling <firstnameDOTlasnameATgw-computingDOTnet>
pkgname=jm
pkgver=18.6
pkgrel=1
pkgdesc="H.264/AVC reference software"
arch=('i686' 'x86_64')
url="http://iphome.hhi.de/suehring/tml/"
license=('Custom')
depends=('gcc-libs')
makedepends=('gcc')
source=("http://iphome.hhi.de/suehring/tml/download/jm${pkgver}.zip"
        "http://iphome.hhi.de/suehring/tml/download/COPYRIGHT_ITU.txt"
        "http://iphome.hhi.de/suehring/tml/download/COPYRIGHT_ISO_IEC.txt")

build() {
  cd "${srcdir}/JM"
  chmod +x unixprep.sh && ./unixprep.sh

  tomake=( ldecod lencod rtpdump rtp_loss )
  for _prog in ${tomake[@]}
  do
     cd "${srcdir}/JM/${_prog}"
     sed -i s/-march=pentium4//g Makefile
     make
  done
}
md5sums=('3bb3ce66316fd9e8ec3d26d88319a6ba'
         'eefe0252fdc3fc63e363aa2fb96e66da'
         '5505e5260a127a7e206601323f6c6c25')

package() {
  install -D -m 644 "${srcdir}/JM/Readme.txt" "${pkgdir}/usr/share/doc/${pkgname}/Readme.txt"
  install -D -m 644 "${srcdir}/JM/CHANGES.TXT" "${pkgdir}/usr/share/doc/${pkgname}/CHANGES.txt"
  install -D -m 644 "${srcdir}/JM/Changes_detail.txt" "${pkgdir}/usr/share/doc/${pkgname}/Changes_detail.txt"
  install -D -m 644 "${srcdir}/JM/FREXT_changes.txt" "${pkgdir}/usr/share/doc/${pkgname}/FREXT_changes.txt"
  install -D -m 644 "${srcdir}/JM/disclaimer.txt" "${pkgdir}/usr/share/doc/${pkgname}/disclaimer.txt"

  cd "${srcdir}/JM/bin"

  runtimes=( ldecod lencod rtpdump rtp_loss )
  for _prog in ${runtimes[@]}
  do
     install -D -m 755 "${_prog}.exe" "${pkgdir}/usr/bin/${_prog}"
  done
  cfgs=( decoder decoder_stereo encoder encoder_baseline encoder_extended encoder_main encoder_max_performance encoder_stereo encoder_tonemapping encoder_view1 encoder_yuv422 explicit_seq leakybucketrate q_matrix q_matrix2 q_matrix_def q_offset sg0conf sg2conf sg6conf )
  for _cfg in ${cfgs[@]}
  do
    install -D -m 644 "${_cfg}.cfg"  "${pkgdir}/usr/share/doc/${pkgname}/cfg/${_cfg}.cfg"
  done

  install -D -m 644 "${srcdir}/COPYRIGHT_ITU.txt" "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT_ITU.txt"
  install -D -m 644 "${srcdir}/COPYRIGHT_ISO_IEC.txt" "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT_ISO_IEC.txt"
}
