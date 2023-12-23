# Maintainer: Devin Lin <devin@kde.org>
pkgbase=plasma-mobile
pkgver=5.27.10
pkgrel=2
pkgdesc="Plasma Mobile shell components."
arch=(x86_64 i686 i486 pentium4 arm armv6h armv7h aarch64)
url="https://invent.kde.org/plasma/plasma-mobile"
license=('GPL3')
groups=()

pkgname=(
  qqc2-breeze-style
  plasma-mobile
)


optdepends=(
  'plasma-mobile-nm: Mobile networking settings modules for WiFi, etc.'
  'plasma-settings: Settings application for Plasma Mobile'
  'plasma-dialer: Phone application'
  'plasma-workspace-wallpapers: A large wallpaper selection for Plasma'
  'plasma-mobile-sounds: Plasma Mobile sound theme'
)
makedepends=(cmake extra-cmake-modules)
source=(
    "https://download.kde.org/stable/plasma/$pkgver/plasma-mobile-$pkgver.tar.xz"
    "https://invent.kde.org/plasma/qqc2-breeze-style/-/archive/0701295ed55e0e7d6dcecca138f67997ebf8c82a/qqc2-breeze-style-0701295ed55e0e7d6dcecca138f67997ebf8c82a.tar.bz2"
)
sha256sums=(
    '2ca8ff8cd848b727e5513ac3edca8fa5ad3618845642eb3f72c5dd5441425b2e'
    'SKIP'
)

prepare() {
  mkdir -p build
}

build() {
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -B qqc2-breeze-style_build -S "qqc2-breeze-style-0701295ed55e0e7d6dcecca138f67997ebf8c82a"
  cmake --build qqc2-breeze-style_build --config Release

  cmake -B plasma-mobile_build -S "plasma-mobile-${pkgver}" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=/usr/lib \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DBUILD_TESTING=OFF
  cmake --build plasma-mobile_build
}

package_plasma-mobile() {
  depends=(
    plasma-nano
    plasma-nm
    plasma-pa
    powerdevil
    modemmanager-qt5
    plasma-wayland-session
    kiconthemes
    kirigami2
    qt5-feedback
    kirigami-addons5
    maliit-keyboard
    kpipewire
  )

  DESTDIR="$pkgdir" cmake --install plasma-mobile_build
}
 

package_qqc2-breeze-style() {
  DESTDIR="${pkgdir}" cmake --install qqc2-breeze-style_build --config Release
}