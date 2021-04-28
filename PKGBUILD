# Maintainer: S Stewart <tda@null.net>
# Maintainer: Cranky Supertoon <crankysupertoon@gmail.com>
# Special thanks to RyanTheAllmighty for making hyper-appimage
pkgname="gdlauncher-bin"
_pkgname="gdlauncher"
pkgver="1.1.5"
pkgrel=1
arch=('x86_64')
pkgdesc="GDLauncher is simple, yet powerful Minecraft custom launcher with a strong focus on the user experience"
url="https://gdevs.io"
license=('GPL3')
makedepends=('gendesk' 'unzip' 'wget')
depends=('libnotify' 'libxss' 'libxtst' 'libindicator-gtk3' 'libappindicator-gtk3')
conflicts=('gdlauncher-appimage' 'gdlauncher' 'gdlauncher-git')
source_x86_64=(
    "GDLauncher-${pkgver}.zip::https://github.com/gorilla-devs/GDLauncher/releases/download/v${pkgver}/GDLauncher-linux-setup.zip"
    "icon.png::https://github.com/gorilla-devs/GDLauncher/raw/master/public/icon.png"
)
noextract=(
    "GDLauncher-${pkgver}.zip"
)

md5sums_x86_64=('f13b28569a9670d639d2e47a4cbd6a4c' 'af0ce1364e34f49af3793bf8193c5369')

prepare() {
    # Manually extract to subfolder
    cd $srcdir
    unzip "GDLauncher-${pkgver}.zip" -d "${pkgname}"
    cp "icon.png" "${pkgname}/icon.png"
    
    # Fix permissions
    find "${pkgname}" -type f ! -name "gdlauncher" -exec chmod 644 {} \;

    # Generate .desktop
    gendesk --pkgname "GDLauncher" --pkgdesc "${pkgdesc}" --icon ${pkgname} --exec "/usr/bin/${pkgname}" -n -f
    mv "GDLauncher.desktop" "${pkgname}/${pkgname}.desktop"
}

package() {
    # Create folders
    install -dm755 "${pkgdir}/opt"
    install -dm755 "${pkgdir}/usr/bin"
    install -dm755 "${pkgdir}/usr/share/icons"
    install -dm755 "${pkgdir}/usr/share/applications"

    # install the main files to /opt
    cp -Rr "${srcdir}/${pkgname}" "${pkgdir}/opt/${pkgname}"

    # link the binary, desktop file, and icon
    ln -sr "${pkgdir}/opt/${pkgname}/${_pkgname}" "${pkgdir}/usr/bin/${pkgname}"
    ln -sr "${pkgdir}/opt/${pkgname}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
    ln -sr "${pkgdir}/opt/${pkgname}/icon.png" "${pkgdir}/usr/share/icons/${pkgname}.png"
}
