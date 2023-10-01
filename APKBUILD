# Contributor:
# Maintainer:
pkgname=box64
pkgver=0.2.4
pkgrel=0
pkgdesc="Linux Userspace x86_64 Emulator with a twist, targeted at ARM64 Linux devices"
url="https://github.com/ptitSeb/box64"
arch="aarch64"
license="MIT License"
depends=""
makedepends="cmake gcc samurai"
checkdepends=""
install=""
subpackages=""
source="$pkgname-$pkgver.tar.gz::https://github.com/ptitSeb/$pkgname/archive/refs/tags/v$pkgver.tar.gz"
builddir="$srcdir/$pkgname-$pkgver"

build() {
	if [ "$CBUILD" != "$CHOST" ]; then
		local crossopts="-DCMAKE_SYSTEM_NAME=Linux -DCMAKE_HOST_SYSTEM_NAME=Linux"
	fi
	cmake -B build -G Ninja \
		-D ARM64=1 \
		-D CMAKE_BUILD_TYPE=Releasei \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_INSTALL_LIBDIR=lib \
		-DBUILD_SHARED_LIBS=ON \
		-DCMAKE_BUILD_TYPE=None \

		$crossopts
	cmake --build build
}

check() {
	ctest --test-dir build --output-on-failure
}

package() {
	DESTDIR="$pkgdir" cmake --install build
}

sha512sums="
8811497934dbc9ea64bae1f26ebea35be2f2d32fbbe14376f689398c80dab77691e9f9ab931382be2501c97acf6d468089803c39845d91bc3d976deef2ea0dd4  box64-0.2.4.tar.gz
"
