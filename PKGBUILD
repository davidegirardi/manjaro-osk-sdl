# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Clayton Craft <clayton@craftyguy.net>
# Contributor: Oliver Smith <ollieparanod@postmarketos.org>

pkgname=osk-sdl
pkgver=0.63
pkgrel=1
pkgdesc="Onscreen keyboard for unlocking LUKS devices"
url="https://gitlab.com/postmarketOS/osk-sdl"
arch=('aarch64')
license=("GPL-3.0-or-later")
depends=('cryptsetup' 'mesa' 'ttf-dejavu')
makedepends=('cryptsetup' 'linux-headers' 'meson' 'scdoc' 'sdl2' 'sdl2_ttf')
source=("https://gitlab.com/postmarketOS/osk-sdl/-/archive/$pkgver/osk-sdl-$pkgver.tar.gz")
options=(!strip)

prepare() {
    mkdir -p build
    #fix font in config
    sed -i s@'/usr/share/fonts/ttf-dejavu/DejaVuSans.ttf'@'/usr/share/fonts/noto/NotoSans-Regular.ttf'@g ${srcdir}/${pkgname}-${pkgver}/osk.conf
}

build() {
    cd "$pkgname-$pkgver"
	arch-meson build
	meson compile ${JOBS:+-j ${JOBS}} -C build
}

package() {
    cd "$pkgname-$pkgver"
	DESTDIR="$pkgdir" meson install --no-rebuild -C build
}

md5sums=('ba068c95e616b2c9ea618a64a934e28a')
