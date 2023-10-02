# Contributor:
# Maintainer:
pkgname=box64
pkgver=0.2.4
pkgrel=0
pkgdesc="Linux Userspace x86_64 Emulator with a twist, targeted at ARM64 Linux devices"
url="https://github.com/ptitSeb/box64"
arch="aarch64 riscv64 ppc64le x86_64"
license="MIT License"
depends="musl-fts musl-obstack"
makedepends="cmake gcc samurai linux-headers musl-fts-dev musl-obstack-dev"
checkdepends=""
install=""
subpackages=""
source="$pkgname-$pkgver.tar.gz::https://github.com/ptitSeb/$pkgname/archive/refs/tags/v$pkgver.tar.gz
        musl.patch
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
c3dd5bc922141b34845730e8aa42f7a16e629a2011d3e585bb44c013df0c0baff46faa8ff5f8232df0e3e119455b27146fa443d0638e817fe8967d56c52eff67  musl.patch
"
