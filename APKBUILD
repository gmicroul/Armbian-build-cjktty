# Reference: <https://postmarketos.org/devicepkg>
# Maintainer: Caleb Connolly <caleb@connolly.tech>

pkgname=device-oneplus-fajita
pkgdesc="OnePlus 6T"
pkgver=14
pkgrel=0
url="https://postmarketos.org"
license="MIT"
arch="aarch64"
options="!check !archcheck"
depends="
	linux-postmarketos-qcom-sdm845
	mkbootimg
	postmarketos-base
	soc-qcom-sdm845
	soc-qcom-sdm845-ucm
	soc-qcom-sdm845-qbootctl
"
makedepends="devicepkg-dev"
source="
	10-unl0kr.conf
	deviceinfo
	hexagonrpcd.confd
	modules-initfs
	q6voiced.conf
	81-libssc-oneplus-fajita.rules
"
subpackages="$pkgname-nonfree-firmware:nonfree_firmware $pkgname-pmtest"

build() {
	devicepkg_build $startdir $pkgname
}

package() {
	devicepkg_package $startdir $pkgname

	install -Dm644 "$srcdir"/10-unl0kr.conf \
		"$pkgdir"/etc/unl0kr.conf.d/10-unl0kr.conf
}

nonfree_firmware() {
	pkgdesc="Modem, WiFi and GPU Firmware, also needed for osk-sdl"
	depends="
		firmware-oneplus-sdm845>=9
		hexagonrpcd
		soc-qcom-sdm845-nonfree-firmware
		soc-qcom-sdm845-modem
	"
	replaces="hexagonrpcd-openrc"
	install="$subpkgname.post-install $subpkgname.post-upgrade"
	mkdir "$subpkgdir"

	install -Dm644 q6voiced.conf "$subpkgdir"/etc/conf.d/q6voiced
	install -Dm644 "$srcdir"/81-libssc-oneplus-fajita.rules -t "$subpkgdir"/usr/lib/udev/rules.d/
	install -Dm644 "$srcdir"/hexagonrpcd.confd "$subpkgdir"/etc/conf.d/hexagonrpcd-sdsp
}

pmtest() {
	depends="bootrr qrtr firmware-oneplus-sdm845 unl0kr"
	install_if="$pkgname=$pkgver-r$pkgrel postmarketos-mkinitfs-hook-ci"
	install="$subpkgname.post-install"

	devicepkg_pmtest_post_install "ttyMSM0,115200" > "$subpkgname.post-install"
}

sha512sums="
e957b7b0ed219eaa56be6c6b976b60886f73970703fdebf045800154ee652affee4e19654b3ac4244b29bcf6760ad3db6cb87143dc9c4673e905800d751103d1  10-unl0kr.conf
07e3d79715befccd1e7393908c06f88ac8468d1ce6cb96138e3a04e6f8274889db169f5daf05b04b633bcc9e85d11ea5c2017b84bc0ae86a8fad80b05794d0d8  deviceinfo
6b5308471fcbb938ac00d6e9a3f8e61073bda1d608f2edf1a2aba4b256dd3f76b1ccee0873dcaa8dc4a8db304d433360a56fe447d70f57ba068428b75ddea236  hexagonrpcd.confd
ea8709aa214cffaefb1d486c0c47044537446faebff16efb3b015623f043f730b7121e401c676e43aa8868bd6c630fc8a2d7dbf5fb082490e9b5493e0405b66d  modules-initfs
fe9871c325a38c0cadc9631870801ec15ab9f5b786ee854325b93eb3d23e7d8b1ac4f1075572ffcd225d8ec514dec09b986972ddff12a89260c0218af6de7887  q6voiced.conf
f4961015c920c50182d35767de080f16ec348ff693a8cca91dd2593640cf19c31c1e6eac1e8a12a1d38946755eb21bdacad29c9e972adaec854500ab3a7ad3a0  81-libssc-oneplus-fajita.rules
"
