# Maintainer: Dan Johansen <strit@manjaro.org>
# Contributor: Clayton Craft <clayton@craftyguy.net>
# Contributor: Oliver Smith <ollieparanod@postmarketos.org>
# Contributor: Davide Girardi <davidegirardi@someknowngooglesmtp.tld>

pkgname=osk-sdl
pkgver=0.63
pkgrel=2
pkgdesc="Onscreen keyboard for unlocking LUKS devices"
url="https://gitlab.com/postmarketOS/osk-sdl"
arch=('aarch64')
license=("GPL-3.0-or-later")
depends=('cryptsetup' 'mesa' 'ttf-dejavu')
makedepends=('cryptsetup' 'linux-headers' 'meson' 'scdoc' 'sdl2' 'sdl2_ttf')
source=(
    "https://gitlab.com/postmarketOS/osk-sdl/-/archive/$pkgver/osk-sdl-$pkgver.tar.gz"
    osk-sdl.hook
    osk-sdl.hook-install
)
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
    mkdir -p "${pkgdir}/usr/lib/initcpio/hooks"
    mkdir -p "${pkgdir}/usr/lib/initcpio/install"
    install -m 644 "${srcdir}/osk-sdl.hook" "${pkgdir}/usr/lib/initcpio/hooks/osk-sdl"
    install -m 644 "${srcdir}/osk-sdl.hook-install" "${pkgdir}/usr/lib/initcpio/install/osk-sdl"
}

md5sums=(
    'ba068c95e616b2c9ea618a64a934e28a'
    'd778df5d55b7dd45d1b2747ba0309d65'
    '80cd741e8c0aeb1590d913b9f8800e9b'
)
