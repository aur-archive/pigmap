# Contributor: T-T

pkgname='pigmap'
pkgver='1.2'
pkgrel=2
pkgdesc="Minecraft Google map generator"
arch=('i686' 'x86_64')
url="https://github.com/equalpants/pigmap"
license=('GPL')
depends=(bash libpng)
makedepends=()
conflicts=()
optdepends=()

source=("https://github.com/equalpants/pigmap/zipball/v$pkgver")
md5sums=(e9c49d3ecb9fd1bf53e868725f309ce6)

build() {
	src="$(dir ${srcdir} -1 | grep equalpants-pigmap)"
	
	cd "${src}"
	mkdir "${pkgdir}/usr"
	mkdir "${pkgdir}/usr/share"
	mkdir "${pkgdir}/usr/share/pigmap"
	mkdir "${pkgdir}/usr/share/pigmap/images"
	mkdir "${pkgdir}/usr/bin"
	make
	cd "${srcdir}"
	for soubor in fire endportal; do
		mv "./${src}/${soubor}.png" "${pkgdir}/usr/share/pigmap/images"
	done
	until [ -e "${srcdir}/../terrain.png" ]; do
		echo -ne "\rCopy terrain.png from your ~/.minecraft/bin/minecraft.jar to package dir (dir with PKGBUILD)."
		sleep 0.5
	done
	for i in chest enderchest largechest; do
		until [ -e "${srcdir}/../$i.png" ]; do
			echo -ne "\rCopy $i.png from your ~/.minecraft/bin/minecraft.jar/item to package dir (dir with PKGBUILD)."
			sleep 0.5
		done
	done
	echo ''
	for i in terrain chest enderchest largechest; do
		cp "${srcdir}/../$i.png" "${pkgdir}/usr/share/pigmap/images"
	done
	for soubor in "${src}/"*; do
		mv "${soubor}" "${pkgdir}/usr/share/pigmap"
	done
	
	echo '#!/bin/bash

cd /usr/share/pigmap
./pigmap $@
' > "${pkgdir}/usr/bin/pigmap"
	chmod +x "${pkgdir}/usr/bin/pigmap"
}
