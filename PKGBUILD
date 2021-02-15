# Maintainer: Dan Johansen <strit@manjaro.org>
# Maintainer: Philip Müller <philm@manjaro.org>
# Maintainer: Danct12 <danct12@disroot.org>
# Contributor: Sam Whited <sam@samwhited.com>

pkgname=feedbackd
pkgver=0.0.0+git20210125
pkgrel=2
pkgdesc="A daemon to provide haptic (and later more) feedback on events"
url="https://source.puri.sm/Librem5/feedbackd"
arch=('x86_64' 'armv7h' 'aarch64')
license=('GPL')
depends=('gobject-introspection' 'gsound' 'json-glib' 'libgudev')
makedepends=('meson' 'vala')
_fbdthemes_commit="1602d415aed30b1a67c0ff270551230725b8ef92" # branch/master
source=(https://source.puri.sm/Librem5/${pkgname}/-/archive/v${pkgver}/${pkgname}-v${pkgver}.tar.gz
	https://source.puri.sm/Librem5/feedbackd-device-themes/-/archive/1602d415aed30b1a67c0ff270551230725b8ef92/feedbackd-device-themes-${_fbdthemes_commit}.tar.gz)

build() {
	arch-meson ${pkgname}-v${pkgver} output
	ninja -C output
}

package() {
	DESTDIR="$pkgdir" ninja -C output install
	install -Dm644 "$srcdir"/${pkgname}-v${pkgver}/debian/feedbackd.udev \
		"$pkgdir"/usr/lib/udev/rules.d/90-feedbackd.rules
	sed -i 's/libexec/lib/g' "$pkgdir"/usr/lib/udev/rules.d/90-feedbackd.rules

	# FIXME: We aren't supposed to abuse video group, but we need to find a
	#        efficient way to add user to feedbackd group.
	sed -i 's/-G feedbackd/-G video/g' "$pkgdir"/usr/lib/udev/rules.d/90-feedbackd.rules

	# It would make much more sense to bundle fbd device configuration with the pkg.
	find ${srcdir}/feedbackd-device-themes-${_fbdthemes_commit}/data -name \*.json \
		 -exec cp {} ${pkgdir}/usr/share/feedbackd/themes \;
}

sha256sums=('48db1e6e8263025d881cd00e66c2d2a82db0d1a632cfb378803f9e3337c5dd8d'
            'afc62d540575b7cd4286935774d532611086f4556a21a03fdd37e983d6e31061')
