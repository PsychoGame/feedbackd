# Maintainer: Dan Johansen <strit@manjaro.org>
# Maintainer: Philip Müller <philm@manjaro.org>
# Contributor: Sam Whited <sam@samwhited.com>

pkgname=feedbackd
pkgver=0.0.0+git20201114
pkgrel=1
pkgdesc="A daemon to provide haptic feedback on events"
url="https://source.puri.sm/Librem5/feedbackd"
license=(GPL3 LGPL3)
arch=('i686' 'x86_64' 'armv6h' 'armv7h' 'aarch64')
depends=(dconf
         gsound
         json-glib
         libgudev)
makedepends=(gobject-introspection
             meson
             pkg-config
             vala)
provides=(libfeedback
          purism-feedbackd
          purism-libfeedback)
source=("https://source.puri.sm/Librem5/${pkgname}/-/archive/v${pkgver}/${pkgname}-v${pkgver}.tar.gz")
sha256sums=('e5da62d70906a9d92cdcfe7d04fe7d3131a4475a9b39599f27ac2da89b15de59')

build() {
	rm -rf build
	arch-meson "${pkgname}-v${pkgver}" build -Dexamples=false -Dgtk_doc=true
	ninja -C build
}

package() {
	DESTDIR="${pkgdir}" ninja -C build install
	install -Dm644 "$srcdir"/${pkgname}-v${pkgver}/debian/feedbackd.udev \
		"$pkgdir"/usr/lib/udev/rules.d/90-feedbackd.rules
}
