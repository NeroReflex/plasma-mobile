# Maintainer: Devin Lin <devin@kde.org>
pkgbase=plasma-mobile
pkgver=5.27.10
pkgrel=3
pkgdesc="Plasma Mobile shell components."
arch=(x86_64 i686 i486 pentium4 arm armv6h armv7h aarch64)
url="https://invent.kde.org/plasma/plasma-mobile"
license=('GPL3')
groups=()

pkgname=(
  qqc2-breeze-style
  plasma-mobile
  plasma-mobile-sounds
  plasma-mobile-nm
)

makedepends=(
    git
    cmake
    extra-cmake-modules
    qt5-tools
)

optdepends=(
  'plasma-settings: Settings application for Plasma Mobile'
  'plasma-dialer: Phone application'
  'plasma-workspace-wallpapers: A large wallpaper selection for Plasma'
)
makedepends=(cmake extra-cmake-modules)
source=(
    "https://download.kde.org/stable/plasma/$pkgver/plasma-mobile-$pkgver.tar.xz"
    "https://download.kde.org/stable/plasma/5.27.10/qqc2-breeze-style-5.27.10.tar.xz"
    "https://download.kde.org/stable/plasma-mobile-sounds/0.1/plasma-mobile-sounds-0.1.tar.xz"
    "https://download.kde.org/stable/plasma/$pkgver/plasma-nm-$pkgver.tar.xz"
)
sha256sums=(
    '2ca8ff8cd848b727e5513ac3edca8fa5ad3618845642eb3f72c5dd5441425b2e'
    '3d8a6fbe18f7ac56ff0c0706e9219df29d49ff398173522bd53f1d8baa7b8b3b' # qqc2-breeze-style-5.27.10.tar.xz
    'f1aed3ddd1de209e0d60df54e968b141b4c868ff0c4706dedb85e4cce29f26af' # plasma-mobile-sounds-0.1.tar.xz
    'b75dd3a7624e137ce350f438c3e3535c24d015d0e096e8e2f513b75df1b3dcb0' # plasma-nm-5.27.10.tar.xz
)

prepare() {
  mkdir -p build
}

build() {
  cmake -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -B qqc2-breeze-style_build \
    -S "qqc2-breeze-style-${pkgver}"

  cmake -B plasma-mobile_build \
    -S "plasma-mobile-${pkgver}" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=/usr/lib \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DBUILD_TESTING=OFF

  cmake -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -B plasma-mobile-sounds_build \
    -S "plasma-mobile-sounds-0.1"

  cmake -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_TESTING=OFF \
    -DBUILD_MOBILE=True \
    -S "plasma-nm-$pkgver" \
    -B plamsa-mobile-nm_build

  cmake --build qqc2-breeze-style_build --config Release
  cmake --build plasma-mobile_build
  cmake --build plasma-mobile-sounds_build --config Release
  cmake --build plamsa-mobile-nm_build --config Release
}

package_plasma-mobile-nm() {
  DESTDIR="$pkgdir" cmake --install plamsa-mobile-nm_build --config Release
}

package_plasma-mobile() {
  depends=(
    plasma-nano
    plasma-nm
    plasma-pa
    powerdevil
    modemmanager-qt5
    plasma-wayland-session
    kirigami2
    qt5-feedback
    kirigami-addons5
    maliit-keyboard
    kpipewire
  )

  DESTDIR="$pkgdir" cmake --install plasma-mobile_build --config Release
}
 

package_qqc2-breeze-style() {
  depends=(
    qt5-base
    qt5-declarative
    qt5-quickcontrols2
    kirigami2
  )

  DESTDIR="${pkgdir}" cmake --install qqc2-breeze-style_build --config Release
}

package_plasma-mobile-sounds() {
  depends=(
    qt5-base
    qt5-declarative
    qt5-quickcontrols2
    kirigami2
  )

  DESTDIR="$pkgdir" cmake --install plasma-mobile-sounds_build --config Release
}