# Maintainer: Qiang <lq95v5@gmail.com>
pkgname=xivlauncher-cn
pkgver=1.0.1.0
_pkgver=ae08df3a025c8178d104ba8356cdb90b82362539
pkgrel=1
pkgdesc="Custom launcher for FFXIV CN"
arch=('x86_64')
url='https://github.com/ottercorp/FFXIVQuickLauncher/'
license=('GPL')
depends=(
    'aria2'
    'sdl2' 'lib32-sdl2'
    'libsecret'
    'attr'                  'lib32-attr'
    'fontconfig'            'lib32-fontconfig'
    'lcms2'                 'lib32-lcms2'
    'libxml2'               'lib32-libxml2'
    'libxcursor'            'lib32-libxcursor'
    'libxrandr'             'lib32-libxrandr'
    'libxdamage'            'lib32-libxdamage'
    'libxi'                 'lib32-libxi'
    'gettext'               'lib32-gettext'
    'freetype2'             'lib32-freetype2'
    'glu'                   'lib32-glu'
    'libsm'                 'lib32-libsm'
    'gcc-libs'              'lib32-gcc-libs'
    'libpcap'               'lib32-libpcap'
    'faudio'                'lib32-faudio'
    'desktop-file-utils'    'jxrlib'
)
makedepends=('dotnet-sdk>=6' 'python-yaml' 'git')
optdepends=('steam')
options=('!strip')
provides=("xivlauncher=${pkgver}")
conflicts=("xivlauncher")
source=(
    "XIVLauncher.Core::git+https://github.com/ottercorp/XIVLauncher.Core.git"
    "XIVLauncher.desktop"
)
sha512sums=(
    'SKIP'
    '7f6324cb31f99194fdd44c34b49bb3b7f04bad1b6cbb1b914959219b545bc3653643edac29134edebec82de00e36a83d1afdcc3e20f9bdaa9cbff8ceac3f5d16'
)

prepare() {
    cd "${srcdir}/XIVLauncher.Core"
    git submodule update --init --recursive
}

build() {
    mkdir -p "${srcdir}/build"
    mkdir -p "${srcdir}/build/Resources"
    cd "${srcdir}/XIVLauncher.Core/src/XIVLauncher.Core/"
    dotnet publish -r linux-x64 --sc -o "${srcdir}/build" --configuration Release -p:DefineConstants=WINE_XIV_ARCH_LINUX
}

package() {
    install -d "${pkgdir}/usr/bin/"
    install -d "${pkgdir}/opt/XIVLauncher/"
    install -D -m644 "${srcdir}/XIVLauncher.desktop" "${pkgdir}/usr/share/applications/XIVLauncher.desktop"
    install -D -m644 "${srcdir}/XIVLauncher.Core/misc/linux_distrib/512.png" "${pkgdir}/usr/share/icons/hicolor/512x512/apps/xivlauncher.png"
    cp -r "${srcdir}/build/." "${pkgdir}/opt/XIVLauncher/"
    ln -s ../../opt/XIVLauncher/XIVLauncher.Core "${pkgdir}/usr/bin/XIVLauncher.Core"
}
