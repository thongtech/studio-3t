pkgname=studio-3t
_pkgname=studio-3t
pkgver=2024.4.0
pkgrel=1
pkgdesc="The Professional Client, IDE and GUI for MongoDB"
arch=('x86_64')
url="https://studio3t.com"
license=("custom")

_source_filename="${_pkgname}-linux-x64.tar.gz"
source=("https://download.studio3t.com/studio-3t/linux/${pkgver}/${_source_filename}")
sha256sums=('56541a31034856333c6fdc634f082b8bb8b06eb695931170cfb23378370a297c')

prepare() {
  # Extract, rename and add execution permision
  tar xzvf ${_source_filename} && for file in *.sh; do mv "$file" ${_pkgname}.sh; done && chmod +x ${_pkgname}.sh

  # unattended mode
  sh ./${_pkgname}.sh -q -dir ${srcdir}/${_pkgname} -overwrite
}

package() {
    # Copy package files
    echo "Copying package files..."
    mkdir -p "${pkgdir}/opt/${_pkgname}"
    install -Dm644 "${srcdir}/${_pkgname}/.install4j/Studio-3T.png" "${pkgdir}/usr/share/pixmaps/${_pkgname}.png"
    cp -R ${_pkgname}/. ${pkgdir}/opt/${_pkgname}

    # Add package to /usr/bin/
    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/opt/${_pkgname}/Studio-3T" "${pkgdir}/usr/bin/${_pkgname}"

    # Copy .desktop file
    mkdir -p "${pkgdir}/usr/share/applications"
    cat << EOF > "${pkgdir}/usr/share/applications/${_pkgname}.desktop"
[Desktop Entry]
Type=Application
Name=Studio 3T
Comment=${pkgdesc}
Exec=${_pkgname}
Icon=${_pkgname}
Terminal=false
StartupNotify=false
Categories=Development;Application;
EOF
}
