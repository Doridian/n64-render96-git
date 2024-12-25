# Maintainer: Doridian <archlinux at doridian dot net>

pkgname=n64-render96-git
pkgver=r769.cd02b888
pkgrel=1
pkgdesc='Recompilation of Super Mario 64 for modern systems'
arch=('any')
url='https://github.com/Render96/Render96ex'
license=('Commercial') # As the built artifact includes the ROM or resources derived from it
makedepends=('git' 'lsb-release' 'audiofile' '7zip' 'unzip')
depends=('sdl2' 'glew')
options=('!strip' '!debug')
source=(
    "${pkgname}::git+${url}#branch=alpha"
    "models.7z::https://github.com/Render96/ModelPack/releases/download/3.2/Render96_DynOs_v3.2.7z"
    "textures-git::git+https://github.com/pokeheadroom/RENDER96-HD-TEXTURE-PACK.git"
    'baserom.us.z64' # Copyrighted, you have to find this yourself, make sure to check on https://2ship.equipment/
    'n64-render96-git.desktop'
    'logo.png'
)
sha256sums=(
    'SKIP'
    'd95ef25a694b1cd2e82785418aebf2aa8fd3a6b394b350fe51971474d19664b2'
    'SKIP'
    '17ce077343c6133f8c9f2d6d6d9a4ab62c8cd2aa57c40aea1f490b4c8bb21d91'
    'SKIP'
    'SKIP'
)

pkgver() {
  cd "${srcdir}/${pkgname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${pkgname}"
  cp ../baserom.us.z64 baserom.us.z64

  make
  cp -rfp "${srcdir}/textures-git/gfx" "build/us_pc/res/"
  7z x '-obuild/us_pc/dynos/packs' -aoa "${srcdir}/models.7z"
}

package() {
  cd "${srcdir}/${pkgname}"

  install -Dm644 ../logo.png "${pkgdir}/usr/share/pixmaps/n64-render96-git.png"
  install -Dm644 ../n64-render96-git.desktop "${pkgdir}/usr/share/applications/n64-render96-git.desktop"

  install -Dm755 build/us_pc/sm64.us.f3dex2e "${pkgdir}/opt/n64/render96-git/sm64"
  cp -rfp build/us_pc/res "${pkgdir}/opt/n64/render96-git/res"
  cp -rfp build/us_pc/dynos "${pkgdir}/opt/n64/render96-git/dynos"
  install -Dm644 ../baserom.us.z64 "${pkgdir}/opt/n64/render96-git/baserom.z64"
}

# vim:set ts=2 sw=2 et:
