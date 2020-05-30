# Maintainer: Omar Roth <omarroth@protonmail.com>
pkgname=lsquic
pkgver=2.14.4
pkgrel=0
pkgdesc="LiteSpeed QUIC and HTTP/3 Library"
url="https://github.com/litespeedtech/lsquic"
arch="all"
license="MIT"
depends="boringssl-dev boringssl-static zlib-static libevent-static"
makedepends="cmake git go perl bsd-compat-headers linux-headers"
subpackages="$pkgname-static"
source="v$pkgver.tar.gz::https://github.com/litespeedtech/lsquic/tarball/v2.14.4
ls-qpack-$pkgver.tar.gz::https://github.com/litespeedtech/ls-qpack/tarball/f416138
ls-hpack-$pkgver.tar.gz::https://github.com/litespeedtech/ls-hpack/tarball/8d4b795"
builddir="$srcdir/litespeedtech-$pkgname-1c105cf"

prepare() {
	cp -r -T "$srcdir/litespeedtech-ls-qpack-f416138" "$builddir/src/liblsquic/ls-qpack"
	cp -r -T "$srcdir/litespeedtech-ls-hpack-8d4b795" "$builddir/src/lshpack"
}

build() {
	cmake \
		-DCMAKE_BUILD_TYPE=None \
		-DBORINGSSL_INCLUDE=/usr/include/openssl \
		-DBORINGSSL_LIB_crypto=/usr/lib \
		-DBORINGSSL_LIB_ssl=/usr/lib .
	make lsquic
}

check() {
	make test
}

package() {
	install -d "$pkgdir/usr/lib"
	install -Dm755 src/liblsquic/liblsquic.a "$pkgdir/usr/lib/liblsquic.a"
}
sha512sums="fa1543f2f5e5929c3ce61b989e52001b3a1362215e0ad7f3e593c08d190e1da2d9e3cef4f50e742e3b46b4a8078baf1c3131feb5c24cdd6ea51d3e4dd136f2fb  v$pkgver.tar.gz
1179a620c7625f9a20e082631bb2b06065a5fd2f0c77a29a4db0361fa654af156fd095a399fe4c5c2a360d9c9342ed0601d3f691d098bbc2d88b14cc47c3d931 ls-qpack-$pkgver.tar.gz
a807b95e4a17fde05eb34fc7d5ad69862cb5109908e53e6d1d5912606e9ce8f9022a0a88b0c5a99bccc475e8c96c4174e390c825b86c711b910b199037f560df ls-hpack-$pkgver.tar.gz"
