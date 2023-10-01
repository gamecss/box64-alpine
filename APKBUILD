# Contributor: ptitSeb
# Maintainer: gamecss
pkgname=box64
pkgver=0.2.4
pkgrel=0
pkgdesc="Linux Userspace x86_64 Emulator with a twist, targeted at ARM64 Linux devices"
url="https://github.com/ptitSeb/box64"
arch="aarch64 riscv64 ppc64le x86_64"
license="MIT License"
depends=""
makedepends="cmake gcc samurai"
checkdepends=""
install=""
subpackages=""
source="$pkgname-$pkgver.tar.gz::https://github.com/ptitSeb/$pkgname/archive/refs/tags/v$pkgver.tar.gz
        emu_x64run_musl.patch
        "
builddir="$srcdir/$pkgname-$pkgver"

case "$CARCH" in
aarch64)
  ARCHOPTS="-D ARM64=1"
	;;
riscv64)
  ARCHOPTS="-D RV64=1"
	;;
ppc64le)
  ARCHOPTS="-D PPC64LE=1"
	;;
x86_64)
	ARCHOPTS="-D LD80BITS=1 -D NOALIGN=1"
	;;
esac

build() {
	cmake -B build -G Ninja \
		-DCMAKE_BUILD_TYPE=RelWithDebInfo \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DBUILD_SHARED_LIBS=ON \
    -DNOGIT=1 \
		$ARCHOPTS
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
4849a8a3feac52d80e963e9d19029d9c845505f069ad68c24a4b2516b1205b7fcbbaf7de5d99f7401e7ca8599ec0bf9a1e51b666522274a15f552645ffcdda56  emu_x64run_musl.patch
"
